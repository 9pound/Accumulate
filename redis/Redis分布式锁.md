# Redis分布式锁

- 可重入锁
- 乐观锁
- 公平锁
- 读写锁
- Redlock（红锁，下面会详细讲）

**Redis并不能实现严格意义上的分布式锁。**但是这并不意味着上面讨论的方案一无是处。如果你的应用场景为了效率(efficiency)，协调各个客户端避免做重复的工作，即使锁失效了，只是可能把某些操作多做一遍而已，不会产生其它的不良后果。但是如果你的应用场景是为了正确性(correctness)，那么用Redis实现分布式锁并不合适，会存在各种各样的问题，且解决起来就很复杂，为了正确性，需要使用zab、raft共识算法，或者使用带有事务的数据库来实现严格意义上的分布式锁。

为了保证分布式锁的可用性，至少要确保锁的实现要同时满足以下几点：

- 互斥性。在任何时刻，保证只有一个客户端持有锁。
- 不能出现死锁。如果在一个客户端持有锁的期间，这个客户端崩溃了，也要保证后续的其他客户端可以上锁。
- 保证上锁和解锁都是同一个客户端。

## 单点

setnx命令：在键不存在的情况下为键设置值（互斥性）

### 加锁过程

```redis
SETNX lock 1
```

### 解锁过程

```
DEL lock
```

## 存在的问题

#### 死锁

- 解决方案：设置超时时间

```redis
setnx lock 1    //1、加锁
expire lock 10  //2、加锁
del lock		//3、解锁
```

还是存在以下问题

1、步骤1、2 不是原子的

```
1、在 Redis 2.6.12 之后，Redis 扩展了 SET 命令的参数，用这一条命令就可以了
SET lock 1 EX 10 NX
2、使用lua脚本
```

2、释放别人的锁

```
键的值设置唯一表示，释放锁时先判断，是不是自己持有的锁
// 加锁
SET lock $uuid EX 20 NX

// 解锁
if redis.call("get",KEYS[1]) == ARGV[1] then
    return redis.call("del",KEYS[1])
else
    return 0
end
```

3、锁过期时间不好评估

watchDog机制实现锁的续期。当加锁成功后，同时开启守护线程，默认有效期是30秒，每隔10秒就会给锁续期到30秒，只要持有锁的客户端没有宕机，就能保证一直持有锁，直到业务代码执行完毕由客户端自己解锁，如果宕机了自然就在有效期失效后自动解锁。

#### 不可重入

使用Redis的哈希表存储可重入次数，当加锁成功后，使用`hset`命令，value(重入次数)则是1。

```

hset myLock
8743c9c0-0795-4907-87fd-6c719a6b4586:1 1

incrby myLock
8743c9c0-0795-4907-87fd-6c71a6b4586:1 1
```

## 集群

### RedLock算法


整体的流程是这样的，一共分为5步:

1. 客户端先获取「当前时间戳T1」
2. 客户端依次向这5个Redis 实例发起加锁请求（用前面讲到的SET命令)，且每个请求会设置超时时间（毫秒级，要远小于锁的有效时间)，如果某一个实例加锁失败（包括网络超时、锁被其它人持有等各种异常情况)，就立即向下一个Redis实例申请加锁
3. 如果客户端从>=3个(大多数)以上Redis 实例加锁成功，则再次获取「当前时间戳T2」，如果T2-T1<锁的过期时间，此时，认为客户端加锁成功，否则认为枷锁失败
4. 加锁成功，去操作共享资源（例如修改MySQL某一行，或发起一个API请求)
5. 加锁失败，向「全部节点」发起释放锁请求(前面讲到的 Lua脚本释放锁)

##### 总结：

1.客户端在多个Redis 实例上申请加锁

2.必须保证大多数节点加锁成功

3.大多数节点加锁的总耗时，要小于锁设置的过期时间4.释放锁，要向全部节点发起释放锁请求





获取当前时间戳，单位是毫秒；

跟上面类似，轮流尝试在每个 master 节点上创建锁，过期时间较短，一般就几十毫秒；

尝试在大多数节点上建立一个锁，比如 5 个节点就要求是 3 个节点 n / 2 + 1；

客户端计算建立好锁的时间，如果建立锁的时间小于超时时间，就算建立成功了；

要是锁建立失败了，那么就依次之前建立过的锁删除；

只要别人建立了一把分布式锁，你就得不断轮询去尝试获取锁。



作者：民工哥
链接：https://www.zhihu.com/question/300767410/answer/1980587949
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

#### 原文：

[Distributed locks with Redis – Redis](https://redis.io/topics/distlock)

## The Redlock algorithm

In the distributed version of the algorithm we assume we have N Redis masters. Those nodes are totally independent, so we don’t use replication or any other implicit coordination system. We already described how to acquire and release the lock safely in a single instance. We take for granted that the algorithm will use this method to acquire and release the lock in a single instance. In our examples we set N=5, which is a reasonable value, so we need to run 5 Redis masters on different computers or virtual machines in order to ensure that they’ll fail in a mostly independent way.

In order to acquire the lock, the client performs the following operations:

1. It gets the current time in milliseconds.
2. It tries to acquire the lock in all the N instances sequentially, using the same key name and random value in all the instances. During step 2, when setting the lock in each instance, the client uses a timeout which is small compared to the total lock auto-release time in order to acquire it. For example if the auto-release time is 10 seconds, the timeout could be in the ~ 5-50 milliseconds range. This prevents the client from remaining blocked for a long time trying to talk with a Redis node which is down: if an instance is not available, we should try to talk with the next instance ASAP.
3. The client computes how much time elapsed in order to acquire the lock, by subtracting from the current time the timestamp obtained in step 1. If and only if the client was able to acquire the lock in the majority of the instances (at least 3), and the total time elapsed to acquire the lock is less than lock validity time, the lock is considered to be acquired.
4. If the lock was acquired, its validity time is considered to be the initial validity time minus the time elapsed, as computed in step 3.
5. If the client failed to acquire the lock for some reason (either it was not able to lock N/2+1 instances or the validity time is negative), it will try to unlock all the instances (even the instances it believed it was not able to lock).



### 关于RedLock的问题讨论

- 如果有节点发生崩溃重启

- 如果客户端长期阻塞导致锁过期

- 时钟跳跃问题
- 解决主从切换后，锁失效问题的

https://www.zhihu.com/question/300767410/answer/647252732



## Redisson 实现原理

## 加锁过程

![img](https://pic3.zhimg.com/80/v2-dcb84f1e00349f22c8399535bfd50b2b_720w.jpg?source=1940ef5c)

```java
// 1.构造redisson实现分布式锁必要的Config
Config config = new Config();
config.useSingleServer().setAddress("redis://127.0.0.1:5379").setPassword("123456").setDatabase(0);
// 2.构造RedissonClient
RedissonClient redissonClient = Redisson.create(config);
// 3.获取锁对象实例（无法保证是按线程的顺序获取到）
RLock rLock = redissonClient.getLock(lockKey);
try {
    /**
     * 4.尝试获取锁
     * waitTimeout 尝试获取锁的最大等待时间，超过这个值，则认为获取锁失败
     * leaseTime   锁的持有时间,超过这个时间锁会自动失效（值应设置为大于业务处理的时间，确保在锁有效期内业务能处理完）
     */
    boolean res = rLock.tryLock((long)waitTimeout, (long)leaseTime, TimeUnit.SECONDS);
    if (res) {
        //成功获得锁，在这里处理业务
    }
} catch (Exception e) {
    throw new RuntimeException("aquire lock fail");
}finally{
    //无论如何, 最后都要解锁
    rLock.unlock();
}
```

## 解锁过程

![img](https://pic1.zhimg.com/80/v2-2913e2bafd4daa7dba69fcaf4df11f43_720w.jpg?source=1940ef5c)







如何实现互斥

**watch dog自动延期机制**

如何实现可重入加锁机制





RedissonLock 同样没有解决 节点挂掉的时候

最大缺陷：在redis master实例宕机的时候，可能导致多个客户端同时完成加锁。



参考

[怎样实现redis分布式锁？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/300767410)