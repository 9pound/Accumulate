# AQS

AQS是一个构建锁和同步器的框架，它定义了多线程的环境下线程如何获取锁、释放锁、如何阻塞、如何被唤醒等操作？

#### 功能

独占（ReentrantLock）

​	分公平和非公平

共享 （ReentrantReadWriteLock、Semaphore、CountDownLatch、CyclicBarrier、ReadWriteLock）

#### 源码

```java
      /**
     * Head of the wait queue, lazily initialized.  Except for
     * initialization, it is modified only via method setHead.  Note:
     * If head   exists, its waitStatus is guaranteed not to be
     * CANCELLED.
     */  
    private transient volatile Node head;
  
    /**
     * Tail of the wait queue, lazily initialized.  Modified only via
     * method enq to add new wait node.
     */
    private transient volatile Node tail;

    /**
     * The synchronization state.
     */
    private volatile int state;
    
    /**
     * Returns the current value of synchronization state.
     * This operation has memory semantics of a {@code volatile} read.
     * @return current state value
     */
    protected final int getState() {
        return state;
    }

    /**
     * Sets the value of synchronization state.
     * This operation has memory semantics of a {@code volatile} write.
     * @param newState the new state value
     */
    protected final void setState(int newState) {
        state = newState;
    }

    /**
     * Atomically sets synchronization state to the given updated
     * value if the current state value equals the expected value.
     * This operation has memory semantics of a {@code volatile} read
     * and write.
     *
     * @param expect the expected value
     * @param update the new value
     * @return {@code true} if successful. False return indicates that the actual
     *         value was not equal to the expected value.
     */
    protected final boolean compareAndSetState(int expect, int update) {
        // See below for intrinsics setup to support this
        return unsafe.compareAndSwapInt(this, stateOffset, expect, update);
    }
    
```

[参考](https://segmentfault.com/a/1190000017372067)

