# Synchronized

#### **本质**：

- 对象的内部锁

#### 性质：

- 原子性、可见性、顺序性

- 可重入性

#### 作用：

- java中每个对象都有一个内部锁，并且该锁只有一个内部条件。
- 如果一个方法用synchronized关键字声明，那么锁对象将保护整个方法

#### 使用场景

- 修饰实例方法、锁的是当前实例对象
- 修饰静态方法、锁的是当前类测class对象
- 修饰代码块、锁的是Synchronized括号中指定的对象

#### **原理：**

- ##### **代码块**

  - monitorenter
  - monitorexit
  - monitor 对象存在于对象头中

  在字节码中同步代码块开始的位置加monitorenter，在代码块结束的位置加monitorexit。 

- ##### **在静态方法和方法上**

  - 加锁 ACC—SYCHRONIZED 标识。指明该方法是一个同步方法

#### **缺点**：

- 不能中断一个正在试图获取锁的线程
- 试图获取锁时不能设定超时
- 每个锁仅有单一的条件

#### 条件对象

**wait（）**添加线程到等待集

**notify（）/notifyAll（）**解除等待线程的阻塞状态

****

**总结：**

- 锁用来保护代码片段，任何时刻只能有一个线程执行被保护的代码
- 锁可以管理试图进入被保护代码段的线程
- 锁可以拥有一个或多个条件
- 每个条件对象管理那些已经进入被保护的代码段但还不能运行的线程

#### 锁的四种状态（对应MarkWord结构）

- 无锁状态
- 偏向锁状态
- 轻量级锁状态
- 重量级锁状态

# FAQ

#### synchronized 还有别的作用范围?

- 修饰实例方法
- 修饰静态方法
  - 锁的是类对象的内部锁，例如Bank类，则锁的是Bank.class 对象
- 修饰代码块（同步阻塞）
  - 特点是可以指定锁什么对象

#### synchronized是如何实现的，底层原理（monitorenter，monitorexits）？

#### synchronized 是公平锁还是非公平锁吗？

非公平锁

#### 双重校验锁实现单例模式？

#### synchronized与volatile的区别？

#### synchronized和Reentrantlock之间的区别？

- 都是可重入锁
- 实现方式不同 synchronized 依赖于jvm，Reentrantlock依赖于API
- ReentrantLock 可以实现可等待中断、公平锁、锁可以绑定多条件


#### 不使用synchronized如何实现一个线程安全的单例？

饿汉模式

#### synchronized如何实现原子性？

#### synchronized如何实现可见性？

#### synchronized如何实现有序性？

#### Synchronized锁优化？

#### synchronized 锁状态怎么从无锁状态到偏向锁的吗？

#### 偏向锁撤销升级到轻量级锁的？

#### 轻量级锁什么时候膨胀为重量级锁？





https://blog.csdn.net/guyuealian/article/details/52525724

https://blog.csdn.net/xueba8/article/details/88753443

https://blog.csdn.net/zhengwangzw/article/details/105141484