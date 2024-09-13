# 读/写锁ReentrantReadWritedLock

如果多个线程对一个数据结构读取数据而很少线程修改其中的数据

```

private ReentrantReadWriteLock rwl = new ReentrantReadWriteLock();

private Lock readLock = rwl.readLock();
private Lock writeLock = rwl.writeLock();

public double getTotalBalance() {
	readLock.lock();
	try{
	
	} finally {
		readlock.unlock();
	}
}
public void transfer() {
	writeLock.lock();
	try {
	
	} finally {
		writeLock().unlock();
	}
}
```

读写锁特性：

- 读写锁是写模式加锁时，解锁前，所有对该锁加锁的线程都会阻塞。
- 读写锁是读模式加锁时，如果线程以读模式加锁会成功，如果线程以写模式加锁会阻塞
- 读写锁是读模式加锁时，既有试图以写模式加锁的线程，也有试图以读模式加锁的线程，那么读模式会读阻塞随后的读模式锁请求，优先满足写模式锁，读锁、写锁并行阻塞，写锁优先级高。