## Redis数据结构

### Redis keys

Redis key值是二进制安全的，这意味着可以用任何二进制序列作为key值，从形如”foo”的简单字符串到一个JPEG文件的内容都可以。空字符串也是有效key值。

### 字符串（Strings）

- Redis的字符串就是一个由字节组成的序列。

- 一个字符串类型的值最多能存储512M字节的内容。

- Redis字符串是二进制安全的，这意味着一个Redis字符串能包含任意类型的数据。

  - 字节串
  - 整数
  - 符点数

**数值命令**


|    命令     |          参数          |
| :---------: | :--------------------: |
|     get     |      get key-name      |
|     set     |   set key-name value   |
|     del     |      del key-name      |
|    incr     |     incr key-name      |
|    decr     |     decr key-name      |
|   incrby    | incrby key-name amount |
|   dectby    | dectby key-name amount |
| Incrbyfloat |                        |
|             |                        |



**字符串命令**

|      |      |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |



- incr，decr只能作用于整数。

- ```redis
  127.0.0.1:6379> get string 
  "1.23"
  127.0.0.1:6379> incr string
  (error) ERR value is not an integer or out of range
  127.0.0.1:6379> decr string
  (error) ERR value is not an integer or out of range
  ```

  

- 如果用户对一个不存在的键或者一个保存了空串的键执行自增或者自减操作，那么redis在执行操作时会将这个键的值当做是0来处理，

- 如果对一个值无法被解释为整数或者浮点数的字符串执行自增或者自减操作，那么Redis将返回一个错误

- 即使在设置键时输入的值为字符串，但只要这个值可以被解释为整数，我们就可以把它当做整数来处理

### 列表（Lists）

- list是简单的字符串列表，按照插入顺序排序。
- 一个列表最多可以包含2e32-1个元素（4294967295，每个表超过40亿个元素）。
- 从时间复杂度的角度来看，Redis列表主要的特性就是支持时间常数的 插入和靠近头尾部元素的删除，即使是需要插入上百万的条目。



|  命令  | 说明                                   |
| :----: | -------------------------------------- |
| rpush  | 将给定的值推入列表的右端               |
|  lpop  | 从列表的左端弹出一个值，并返回弹出的值 |
| lrange | 获取列表在给定范围的所有值             |
| lindex | 获取列表在给定位置上的单个元素         |
|        |                                        |
|        |                                        |

- list的起始索引是0，结束索引为-1
- 当对一个空key执行其中某个命令时，将会创建一个新表。
- 如果一个操作要清空列表，那么key会从对应的key空间删除。这是个非常便利的语义， 因为如果使用一个不存在的key作为参数，所有的列表命令都会像在对一个空表操作一样。

### 集合（Sets）

- Redis集合不允许存在相同的元素。向集合中多次添加同一元素，在集合中最终只会存在一个此元素。
- Redis集合是一个无序的字符串合集。你可以**O(1)** 的时间复杂度（无论集合中有多少元素时间复杂度都为常量）完成 添加，删除以及测试元素是否存在的操作。
- 一个集合最多可以包含2e32-1个元素（4294967295，每个集合超过40亿个元素）。

| 命令      | 说明 |
| --------- | ---- |
| sadd      |      |
| smembers  |      |
| sismember |      |
| srem      |      |

- 一个Redis列表十分有趣的事是，它们支持一些服务端的命令从现有的集合出发去进行集合运算。 所以你可以在很短的时间内完成合并（union）,求交(intersection), 找出不同元素的操作。

### **哈希（Hashes或者说散列）**

- Redis Hashes是字符串字段和字符串值之间的映射，所以它们是可以完美的表示对象（eg:一个有名，姓，年龄等属性的用户）的数据类型。

```
@cli
HMSET user:1000 username antirez password P1pp0 age 34
HGETALL user:1000
HSET user:1000 password 12345
HGETALL user:1000
```

-  一个hash最多可以包含2e32-1 个key-value键值对（超过40亿）。

- 一个拥有少量（100个左右）字段的hash需要很少的空间来存储，所有你可以在一个小型的 Redis实例中存储上百万的对象。
- 尽管Hashes主要用来表示对象，但它们也能够存储许多元素，所以你也可以用Hashes来完成许多其他的任务。

  

| 命令    | 行为 |
| ------- | ---- |
| hset    |      |
| hget    |      |
| hgetall |      |
| hdel    |      |

### **有序集合（Sorted sets）**

- 有序集合（Sorted sets）顾名思义，就是有顺序的（sets）。它们的差别是，每个有序集合的成员都关联着一个评分，这个评分用于把有序集 合中的成员按最低分到最高分排列。

- 有序集合中的元素被称为成员，每个成员都拥有一个分值（分值必须为浮点数）。

- 有序集合是redis中唯一 一个既可以根据成员（键）访问元素 ，又可以根据**分值**以及**分值的排列顺序**来访问元素的结构。

  

|               |      |
| ------------- | ---- |
| zadd          |      |
| zrem          |      |
| zrange        |      |
| zrangebyscore |      |
| zcard         |      |
| zincrby       |      |
| zcount        |      |
| zrank         |      |
| zscore        |      |
| zrange        |      |

-  Redis有序集合和Redis集合类似，相同点是都不允许存在相同的元素（但是允许不同的键有相同的分值）。区别是，每个有序集合的成员都关联着一个评分，这个评分用于把有序集合中的成员按最低分到最高分排列。而集合按照插入的顺序排序
- 使用有序集合，你可以非常快地（**O(log(N))**）完成添加，删除和更新元素的操作。 因为元素是在插入时就排好序的，所以很快地通过评分(score)或者 位次(position)获得一个范围的元素。
-  访问有序集合的中间元素同样也是非常快的，你可以轻易地访问任何你需要的东西: 有序的元素，快速的存在性测试，快速访问集合中间元素！ 

### Bitmaps

- Bitmaps本身不是一种数据结构，它是字符串，但是它可以对字符串的位进行操作。
- bitmaps的最大长度是512MB，即2^32个比特位。

```
Bitmaps —
Bitmaps are not an actual data type, but a set of bit-oriented operations defined on the String type. Since strings are binarysafe blobs and their maximum length is 512 MB, they are suitable to set up to 232 different bits.
Bit operations are divided into two groups: constant-time single bit operations , like setting a bit to 1 or 0, or getting its value,and operations on groups of bits, for example counting the number of set bits in a given range of bits(e.g.. populationcounting).
One of the biggest advantages of bitmaps is that they often provide extreme space savings when storing information.Forexample in a system where different users are represented by incremental user IDs, it is possible to remember a single bitinformation (for example, knowing whether a user wants to receive a newsletter) of 4 billion of users using just 512 MB ofmemory.
```

命令

|          |      |
| -------- | ---- |
| setbit   |      |
| getbit   |      |
| BITOP    |      |
| BITCOUNT |      |
| BITPos   |      |

1.BITOP performs bit-wise operations between different strings. The provided operations are AND, OR, XOR and NOT.

2.BITCOUNT performs population counting, reporting the number of bits set to 1.

3.BITPos finds the first bit having the specified value of 0 or 1.

### **HyperLogLogs**

Redis 同样支持 Bitmaps 和 HyperLogLogs 数据类型，实际上是基于字符串的基本类型的数据类型，但有自己的语义。

### **Stream**

是Redis 5.0版本引入的一个新的数据类型，它以更抽象的方式模拟*日志数据结构*，它实现了额外的非强制性的特性：提供了一组允许消费者以阻塞的方式等待生产者向Stream中发送的新消息，允许一组客户端相互配合来消费同一个Stream的不同部分的消息。

**XADD**

\> XADD mystream * sensor-id 1234 temperature 19.8 

1518951480106-0

**XLEN**命令来获取一个Stream的条目数量

|                     |                     |      |
| ------------------- | ------------------- | ---- |
|                     |                     |      |
|                     |                     |      |
| XRANGE 和 XREVRANGE | XRANGE mystream - + |      |

### GEO





[Redis学习笔记(七)：redis高级数据类型及应用场景-Bitmaps、HyperLogLog、GEO - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/47161453425/)

### 总结：

- 二进制安全的字符串
- Lists: 可以**重复**的按**插入顺序**排序的字符串元素的集合。他们基本上就是*链表（linked lists）*。（双向链表）
- Sets: **不重复**且**无序**的字符串元素的集合。
- Sorted sets,类似Sets,但是每个字符串元素都关联到一个叫*score*浮动数值（floating number value）。里面的元素总是通过score进行着排序，所以不同的是，它是可以检索的一系列元素。（例如你可能会问：给我前面10个或者后面10个元素）。
- Hashes,由field和关联的value组成的map。**field和value都是字符串的**。这和Ruby、Python的hashes很像。
- Bit arrays (或者说 simply bitmaps): 通过特殊的命令，你可以将 String 值当作一系列 bits 处理：可以设置和清除单独的 bits，数出所有设为 1 的 bits 的数量，找到最前的被设为 1 或 0 的 bit，等等。
- HyperLogLogs: 这是被用于估计一个 set 中元素数量的概率性的数据结构。别害怕，它比看起来的样子要简单…参见本教程的 HyperLogLog 部分。

### 键的过期时间

需求：让一个键在给定的时限之后自动被删除

好处：清理缓存数据，降低内存占用。

|           |              |
| --------- | ------------ |
| persist   | 去除超时时间 |
| ttl       | 剩余存活时间 |
| expire    | 设置超时时间 |
| expireat  |              |
| pttl      |              |
| pexpire   |              |
| pexpireat |              |



如果设置了超时时间  的键的值被修改， append命令，该超时设置任然会继续

如果在设置了超时时间的键上调用set或setGet命令，那么超时时间会被清除

如果为一个键设置了超时时间，但是此时关闭redis数据库，将数据存储到快照中的话，在超时之后重启Redis数据库会自动驱逐该键



### 



#### 其他命令

exists：判断键是否存在于redis中

type：确定是否是期望的数据结构

keys：

scan：命令抽取一个随机的键片段，然后将提供的模式和MATCH选项应用到此随机片段上，Scan命令的用法仅对小型数据库有效，如果数据库再大一点，Scan可能会无法匹配任何数据或者只返回所有匹配数据的一个子集。

smembers:

### **参考文档**

http://www.redis.cn/topics/data-types-intro.html

http://www.redis.cn/topics/data-types.html

[《Redis实战》](https://www.manning.com/books/redis-in-action)