# Thread

### start()：

```java
public synchronized void start() {
    /**
     * This method is not invoked for the main method thread or "system"
     * group threads created/set up by the VM. Any new functionality added
     * to this method in the future may have to also be added to the VM.
     *
     * A zero status value corresponds to state "NEW".
     */
    if (threadStatus != 0)
        throw new IllegalThreadStateException();

    /* Notify the group that this thread is about to be started
     * so that it can be added to the group's list of threads
     * and the group's unstarted count can be decremented. */
    group.add(this);

    boolean started = false;
    try {
        start0();
        started = true;
    } finally {
        try {
            if (!started) {
                group.threadStartFailed(this);
            }
        } catch (Throwable ignore) {
            /* do nothing. If start0 threw a Throwable then
              it will be passed up the call stack */
        }
    }
}

private native void start0();
```

### run()：

```java

/* What will be run. */
private Runnable target;

@Override
public void run() {
    if (target != null) {
        target.run();
    }
}
```

### sleep()：

```java
public static native void sleep(long millis) throws InterruptedException;
```

### wait()：

想要调用wait方法，前提是必须获取对象上的锁资源

```java
public final native void wait(long timeout) throws InterruptedException;
```

### join()：

等待终止指定线程

```java
public final synchronized void join(long millis)
throws InterruptedException {
    long base = System.currentTimeMillis();
    long now = 0;

    if (millis < 0) {
        throw new IllegalArgumentException("timeout value is negative");
    }

    if (millis == 0) {
        while (isAlive()) {
            wait(0);
        }
    } else {
        while (isAlive()) {
            long delay = millis - now;
            if (delay <= 0) {
                break;
            }
            wait(delay);
            now = System.currentTimeMillis() - base;
        }
    }
}

public final synchronized void join(long millis, int nanos)
throws InterruptedException {

    if (millis < 0) {
        throw new IllegalArgumentException("timeout value is negative");
    }

    if (nanos < 0 || nanos > 999999) {
        throw new IllegalArgumentException(
                            "nanosecond timeout value out of range");
    }

    if (nanos >= 500000 || (nanos != 0 && millis == 0)) {
        millis++;
    }

    join(millis);
}


public final void join() throws InterruptedException {
    join(0);
}
```

### yield()：

使当前线程从执行状态（运行状态）变为可执行态，即使刚刚放弃了执行的权利, 也可能下一次就被调度回来了.

```
public static native void yield();
```

interrupt：

用来请求终止线程，将中断状态设置为true

interrupted：

静态方法，检测当前线程是否被中断，清除该线程的中断状态，将当前线程的中断状态重置为FALSE

isInterrupted：

检测当前线程是否被中断，不改变中断状态

currentThread()：

getState()

setProivity()

setDaemon()

没有强制终止线程的方法（有一个stop但是过时了），

执行return语句返回

没有捕获异常时



Thread.join() :当前线程A等待Thread线程终止之后才从thread.join()，返回



## FAQ

#### start 与 run 区别？

看源码

#### sleep与wait方法的区别？

- wait是Object的方法、sleep是Thread类中的方法
- wait方法会释放已获取的对象锁资源，sleep方法不释放已获取的锁资源
- 调用wait方法后需要通过其他线程调用notify()或者notifyAll()方法唤醒，sleep超时或者调用interrupt()方法体唤醒

|            | wait                                                         | sleep                                             |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------- |
| 同步       | 只能在同步上下文中调用wait方法，否则或抛出IllegalMonitorStateException异常 | 不需要在同步方法或同步块中调用                    |
| 作用对象   | wait方法定义在Object类中，作用于对象本身                     | sleep方法定义在java.lang.Thread中，作用于当前线程 |
| 释放锁资源 | 是                                                           | 否                                                |
| 唤醒条件   | 其他线程调用对象的notify()或者notifyAll()方法                | 超时或者调用interrupt()方法体                     |
| 方法签名   | wait是实例方法                                               | sleep是静态方法                                   |

#### Thread.sleep(0)的作用？Thread.yield()和Thread.sleep(0)的区别？

- 线程暂时放弃cpu，也就是释放一些未用的时间片给其他线程或进程使用，就相当于一个让位动作。

参考[(7条消息) Thread.yield()和Thread.sleep(0)_斜阳雨陌-CSDN博客_thread.yield()和thread.sleep(0)](https://blog.csdn.net/qq_15037231/article/details/103440060)

#### interrupt、interrupted、isInterrupted方法的区别？

|          | interrupt          | interrupted         | isInterrupted  |
| -------- | ------------------ | ------------------- | -------------- |
| 方法签名 |                    |                     |                |
| 中断状态 | 中断状态设置为true | 中断状态重置为false | 不改变中断状态 |
|          |                    |                     |                |

#### 阻塞与等待的区别？

- 被动阻塞、没有获得锁，没有进入临界区
- 主动等待、获得了锁，进入了临界区，暂时释放了锁

#### Java中你怎样唤醒一个阻塞的线程？
