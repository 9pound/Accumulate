# volatile

## 定义

轻量级的synchronized，如果一个字段被声明为volatile，Java线程内存模型确保所有线程看到这个变量的值是一致的。

## 性质

- 可见性：当一个线程修改了这个变量的值，新值对于其他线程来说是可以立即的得知的

- 顺序性：禁止指令重排序优化
- 原子性：对单个volatile变量的读写具有原子性，但是对于volatile++这种复合操作不具有原子性

volatile 不是线程安全的，因为在java里面的运算操作并非原子操作，这导致了volatile变量的运算在并发下是不安全的

### Volatile变量不保证原子性

volatile关键字为实例域的同步访问提供了一种免锁机制。如果声明一个域为volatile，那么编译器和虚拟机就知道该域是可能被另一个线程并发更新

假设对共享变量除了赋值之外并不完成其他操作，那么可以将这些共享变量声明为volatile

### 保证可见性的原理

- Lock指令：对volatile变量进行写操作时会给指令加一个Lock指令， Lock指令引起缓存写回内存（处理器声言 LOCK# 信号锁总线）
- 缓存一直性协议（MESI）：一个处理器缓存写回内存会导致其他处理器的缓存无效

对volatile变量的写操作：会添加Lock指令，Lock指令有两个作用

1、将当前处理器缓存行的数据写会内存

2、写回内存的操作会使在其他cup里缓存了该内存地址的数据无效

缓存一致性协议：每个处理器会通过**嗅探**在总线上传播的数据来检查自己缓存的值是不是过期了，如果过期了就把当前缓存行设置为过期状态，当修改这个数据的时候，会从新从内存中把这个数据读到缓存里

### 保证顺序性的原理

内存屏障

- 在每个volatile写操作的前面插入一个StoreStore屏障
- 在每个volatile写操作的后面插入一个StoreLoad屏障
- 在每个volatile读操作的后面插入一个LoadLoad屏障
- 在每个volatile读操作的后面插入一个LoadStore屏障

## volatile读写内存语义

- 当写一个volatile变量时，JMM会把该线程对应的本地内存中的共享变量值刷新到主内存
- 当读一个volatile变量时，JMM会把该线程对应的本地内存置为无效，线程接下来将从主内存中读取共享变量



- 每次使用前都必须先从主内存中刷新最新的值
- 每次修改后都必须立刻同步会主内存中
- volatile修饰的变量不会被指令重排序优化





### 应用场景



先行发生原则



# FAQ

为什么要用 volatile 修饰？说说它的功能？

什么是 MESI 协议？CPU 原语是什么？

什么是可见性？

JMM 说说是什么？为什么要有 JMM？

[Happened-before](https://en.wikipedia.org/wiki/Happened-before) 是什么？它和 synchronized 的区别是什么？

volatile 是否保证对象内的域，的可见性？

参考

[一个volatile跟面试官扯了半个小时_安琪拉的博客-CSDN博客](https://blog.csdn.net/zhengwangzw/article/details/106060526?spm=1001.2014.3001.5502)

