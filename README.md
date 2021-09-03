## 一、基础篇

### 面向对象

#### 什么是面向对象

[面向对象、面向过程](https://github.com/9pound/Accumulate/blob/master/Java-basic/1%E3%80%81%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E3%80%81%E9%9D%A2%E5%90%91%E8%BF%87%E7%A8%8B.md)

[面向对象的三大基本特征和五大基本原则](https://github.com/9pound/Accumulate/blob/master/Java-basic/%E4%BA%94%E5%A4%A7%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%88%99.md)

[对象的基本特征和对象之间的关系](https://github.com/9pound/Accumulate/blob/master/Java-basic/%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%89%B9%E5%BE%81.md)

#### 平台无关性

Java如何实现的平台无关

JVM还支持哪些语言（Kotlin、Groovy、JRuby、Jython、Scala）

#### 值传递

[值传递、引用传递](https://github.com/9pound/Accumulate/blob/master/Java-basic/%E5%80%BC%E4%BC%A0%E9%80%92%E5%92%8C%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92.md)

为什么说Java中只有值传递

#### 封装、继承、多态

[什么是多态、方法重写与重载](https://github.com/9pound/Accumulate/blob/master/Java-basic/%E4%BB%80%E4%B9%88%E6%98%AF%E5%A4%9A%E6%80%81%E3%80%81%E6%96%B9%E6%B3%95%E9%87%8D%E5%86%99%E4%B8%8E%E9%87%8D%E8%BD%BD%E3%80%81.md)

Java的继承与实现

构造函数与默认构造函数

类变量、成员变量和局部变量

成员变量和方法作用域

[接口和抽象类](https://github.com/9pound/Accumulate/blob/master/Java-basic/%E6%8E%A5%E5%8F%A3%E4%B8%8E%E6%8A%BD%E8%B1%A1%E7%B1%BB%E6%9C%89%E5%93%AA%E4%BA%9B%E5%8C%BA%E5%88%AB.md)

### Java基础知识  

#### 基本数据类型

[8种基本数据类型：整型、浮点型、布尔型、字符型(void也是基本类型)](https://github.com/9pound/Accumulate/blob/master/Java-basic/8%E7%A7%8D%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%EF%BC%884%E7%A7%8D%E6%95%B4%E5%9E%8B%EF%BC%8C2%E7%A7%8D%E6%B5%AE%E7%82%B9%E7%B1%BB%E5%9E%8B%EF%BC%8C1%E7%A7%8D%E5%AD%97%E7%AC%A6%E7%B1%BB%E5%9E%8B%EF%BC%89.md)

整型中byte、short、int、long的取值范围

什么是浮点型？什么是单精度和双精度？为什么不能用浮点型表示金额？

什么自动拆装箱？

什么是包装类型、什么是基本类型、什么是自动拆装箱

基本类型的缓存机制（常量池技术）

#### String

字符串的不可变性

String常用的方法

JDK 6和JDK 7中substring的原理及区别、

replaceFirst、replaceAll、replace区别、

String对“+”的重载、字符串拼接的几种方式和区别

String.valueOf和Integer.toString的区别、

switch对String的支持

字符串池、常量池（运行时常量池、Class常量池）、intern

#### 熟悉Java中各种关键字

transient、instanceof、volatile、synchronized、final、static、const 原理及用法。

#### 集合类

Collection和Collections区别

List、Set、Map、Queue、Stack区别

Arrays.asList获得的List使用时需要注意什么

ArrayList和LinkedList和Vector的区别？

SynchronizedList和Vector的区别？

HashMap、TreeMap、ConcurrentHashMap

HashMap、HashTable、ConcurrentHashMap区别？

HashSet、TreeSet

HashMap与HashSet的区别？

不同版本的JDK中HashMap的实现的区别以及原因？

Set如何保证元素不重复？

- HashSet
- TreeSet

CopyOnWriteArrayList、 

Enumeration和Iterator区别

Java 8中stream相关用法、

apache集合处理工具类的使用

fail-fast 和 fail-safe

#### 枚举

枚举的用法、枚举的实现、枚举与单例、Enum类

Java枚举如何比较

switch对枚举的支持

枚举的序列化如何实现

枚举的线程安全性问题

#### IO

字符流、字节流、输入流、输出流、

同步、异步、阻塞、非阻塞、Linux 5种IO模型

BIO、NIO和AIO的区别、三种IO的用法与原理、netty

#### Java反射与javassist

反射与工厂模式、 反射有什么作用

Class类

```
java.lang.reflect.*
```

#### 动态代理

静态代理、动态代理

动态代理和反射的关系

动态代理的几种实现方式

#### 序列化

什么是序列化与反序列化、为什么序列化、序列化底层原理、序列化与单例模式、protobuf、为什么说序列化并不安全

#### 注解

元注解、自定义注解、Java中常用注解使用、注解与反射的结合

Spring常用注解

#### JMS

什么是Java消息服务、JMS消息传送模型

#### JMX

```
java.lang.management.*`、 `javax.management.*
```

#### 泛型

泛型与继承、类型擦除、泛型中K T V E ？ object等的含义、泛型各种用法

限定通配符和非限定通配符、上下界限定符extends 和 super

List

List<?>和List

#### 单元测

junit、mock、mockito、内存数据库（h2）

#### 正则表达式

```
java.lang.util.regex.*
```

#### 常用的Java工具库

```
commons.lang`, `commons.*...` `guava-libraries` `netty
```

#### API&SPI

API、API和SPI的关系和区别

如何定义SPI、SPI的实现原理

#### 异常

异常类型、正确处理异常、自定义异常

Error和Exception

异常链、try-with-resources

finally和return的执行顺序

#### 时间处理

时区、冬令时和夏令时、时间戳、Java中时间API

格林威治时间、CET,UTC,GMT,CST几种常见时间的含义和关系

SimpleDateFormat的线程安全性问题

Java 8中的时间处理

如何在东八区的计算机上获取美国时间

#### 编码方式

Unicode、有了Unicode为啥还需要UTF-8

GBK、GB2312、GB18030之间的区别

UTF8、UTF16、UTF32区别

URL编解码、Big Endian和Little Endian

如何解决乱码问题

#### 语法糖

Java中语法糖原理、解语法糖

语法糖：switch 支持 String 与枚举、泛型、自动装箱与拆箱、方法变长参数、枚举、内部类、条件编译、 断言、数值字面量、for-each、try-with-resource、Lambda表达式、

### 阅读源代码

String

Integer

Long

Enum

BigDecimal

ThreadLocal、ClassLoader & URLClassLoader、

ArrayList & LinkedList、

HashMap & LinkedHashMap & TreeMap & CouncurrentHashMap、

HashSet & LinkedHashSet & TreeSet

### Java并发编程

#### 并发与并行

什么是并发、什么是并行、并发与并行的区别

#### 线程

- 线程与进程的区别

- 线程的实现

- 线程的声明周期

- 优先级

- 线程调度

- 创建线程的多种方式

- 守护线程


**Thread**

- sleep()方法和wait方法的区别和共同点？
- 常用的方法

**Runnable**

**Callable与Future**

- Runnable接口和Callable接口的区别

#### 监视器

- 什么是监视器
- 特性？

#### final变量

#### volatile

- volatile的实现原理

- happens-before、内存屏障、编译器指令重排和CPU指令重

- volatile和原子性、可见性和有序性之间的关系

- 有了symchronized为什么还需要volatile

- 实现原理

- 同步阻塞

#### ReentrantLock

- 条件对象
- await()/single()/singleAll()方法

##### ReentrantReadWriteLock(读/写锁)

### Synchronized

#### **线程局部变量（ThreadLocal）**

- TheadLoacl内存泄漏问题

#### 

#### 线程安全集合

ConcurrentHashMap

CopyOnWriteArrayList

ConcurrentLinkedQueue

ConcurrentSkipListMap

ConcurrentSkipListSet

ConcurrentLinkedQueue：非阻塞队列(CAS)

BlockingQueue：阻塞队列 (锁)

- 常用的方法
- LinkedBlockingQueue 容量没有上限
- ArrayBlockingQueue 在构造时需要指定容量，还可以指定是否需要公平性，若设置了公平参数，那么等待时间长的线程会优先得到处理

- LinkedBlockingDeque 双端队列
- PriorityBlockQueue 优先级队列，元素按优先级顺序被移除，没有容量上限

- Delayed接口 元素只有在延迟用完的情况下才能从DelayQueue中移除
  - 实现DelayQueue
- TransferQueue接口 允许生产者线程等待，直到消费者准备就绪可以接受一个元素
  - 实现LinkedTransferQueue

#### 同步包装器

Collections.synchronizedList()

Collections.synchronizedMap()

**死锁**

**CAS**

**AQS**

**原子类、java.util.concurrent.atomic包**





#### 执行器

线程池、控制任务组、Fork-Join框架、可完成Future

#### 同步器

信号量、倒计时门栓、障栅、交换器、同步队列

#### 锁

​              锁优化、锁消除、锁粗化、自旋锁、可重入锁、阻塞锁、死锁

#### 线程池

自己设计线程池、submit() 和 execute()、线程池原理

为什么不允许使用Executors创建线程池

#### 线程安全

死锁、死锁如何排查、线程安全和内存模型的关系

### 并发包

#### 阅读源代码，并学会使用

Thread、Runnable、Callable、ReentrantLock、ReentrantReadWriteLock、Atomic*、Semaphore、CountDownLatch、、ConcurrentHashMap、Executors

## 二、底层篇

### JVM

#### JVM内存结构

[运行时数据区：堆、栈、方法区、直接内存、运行时常量池](https://github.com/9pound/Accumulate/blob/master/jvm/Jvm%E7%9A%84%E5%86%85%E5%AD%98%E7%BB%93%E6%9E%84.xmind)

https://www.cnblogs.com/czwbig/p/11127124.html

堆和栈区别

Java中的对象一定在堆上分配吗？不一定（hotspot 的Class对象存放在方法区）

[对象的创建过程](https://github.com/9pound/Accumulate/blob/master/jvm/%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%88%9B%E5%BB%BA%E8%BF%87%E7%A8%8B.xmind)

[对象的内存布局](https://github.com/9pound/Accumulate/blob/master/jvm/%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%B8%83%E5%B1%80.xmind)

[对象的访问定位](https://github.com/9pound/Accumulate/blob/master/jvm/%E5%AF%B9%E8%B1%A1%E7%9A%84%E8%AE%BF%E9%97%AE%E5%AE%9A%E4%BD%8D.md)

#### 垃圾回收

如何判断对象死没死（引用计数、可达性分析）

[垃圾收集算法：标记清除、标记整理、复制算法、分代回收、标记压缩、增量式回收](https://github.com/9pound/Accumulate/blob/master/jvm/%E5%9E%83%E5%9C%BE%E6%94%B6%E9%9B%86%E7%AE%97%E6%B3%95.xmind)

stop the world（GC停顿）

垃圾收集器（CMS、G1、ZGC、Epsilon）

GC参数总结

[内存分配与回收策略](https://github.com/9pound/Accumulate/blob/master/jvm/%E5%86%85%E5%AD%98%E5%88%86%E9%85%8D%E4%B8%8E%E5%9B%9E%E6%94%B6%E7%AD%96%E7%95%A5.xmind)

#### 类文件结构

class文件格式

#### 虚拟机类加载机制

类加载的时机

类的加载过程（加载、验证、准备、解析、初始化）

[类加载器、双亲委派模型、OGSI](https://github.com/9pound/Accumulate/blob/master/jvm/%E7%B1%BB%E5%8A%A0%E8%BD%BD%E5%99%A8.md)

#### Java内存模型

计算机内存模型、缓存一致性、MESI协议

可见性、原子性、顺序性、

happens-before（先行发生原则）

内存屏障、synchronized、volatile、final、锁

#### JVM参数及调优

-Xmx、-Xmn、-Xms、Xss、-XX:SurvivorRatio、

-XX:PermSize、-XX:MaxPermSize、-XX:MaxTenuringThreshold

#### Java对象模型

oop-klass、对象头

#### HotSpot

即时编译器、编译优化

#### 虚拟机性能监控与故障处理工具

jps, jstack, jmap、jstat, jconsole, jinfo, jhat, javap, btrace、TProfiler

Arthas

### 类加载机制

classLoader、类加载过程、双亲委派（破坏双亲委派）、模块化（jboss modules、osgi、jigsaw）

### 编译与反编译

什么是编译（前端编译、后端编译）、什么是反编译

JIT、JIT优化（逃逸分析、栈上分配、标量替换、锁优化）

编译工具：javac

反编译工具：javap 、jad 、CRF

## 三、 进阶篇

### Java底层知识

#### 字节码、class文件格式

#### CPU缓存，L1，L2，L3和伪共享

#### 尾递归

#### 位运算

用位运算实现加、减、乘、除、取余

### 设计模式

设计模式的六大原则：

- 开闭原则（Open Close Principle）

- 里氏代换原则（Liskov Substitution Principle）

- 依赖倒转原则（Dependence Inversion Principle）

- 接口隔离原则（Interface Segregation Principle）

- 迪米特法则（最少知道原则）（Demeter Principle）

- 合成复用原则（Composite Reuse Principle）


#### 了解23种设计模式

创建型模式：单例模式、抽象工厂模式、建造者模式、工厂模式、原型模式。

结构型模式：适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式。

行为型模式：模版方法模式、命令模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式（Interpreter模式）、状态模式、策略模式、职责链模式(责任链模式)、访问者模式。

#### 会使用常用设计模式

单例的七种写法：懒汉——线程不安全、懒汉——线程安全、饿汉、饿汉——变种、静态内部类、枚举、双重校验锁

工厂模式、适配器模式、策略模式、模板方法模式、观察者模式、外观模式、代理模式等必会

#### 不用synchronized和lock，实现线程安全的单例模式

#### nio和reactor设计模式

### 网络编程知识

#### tcp、udp、http、https等常用协议

三次握手与四次关闭、流量控制和拥塞控制、OSI七层模型、tcp粘包与拆包

#### http/1.0 http/1.1 http/2之间的区别

http中 get和post区别

常见的web请求返回的状态码

404、302、301、500分别代表什么

#### http/3

#### Java RMI，Socket，HttpClient

#### cookie 与 session

cookie被禁用，如何实现session

#### 用Java写一个简单的静态文件的HTTP服务器

#### 了解nginx和apache服务器的特性并搭建一个对应的服务器

#### 用Java实现FTP、SMTP协议

#### 进程间通讯的方式

#### 什么是CDN？如果实现？

#### DNS？

什么是DNS 、记录类型:A记录、CNAME记录、AAAA记录等

域名解析、根域名服务器

DNS污染、DNS劫持、公共DNS：114 DNS、Google DNS、OpenDNS

#### 反向代理

正向代理、反向代理

反向代理服务器

### 框架知识

#### Servlet

生命周期

线程安全问题

filter和listener

web.xml中常用配置及作用

#### Hibernate

什么是OR Mapping

Hibernate的缓存机制

Hibernate的懒加载

Hibernate/Ibatis/MyBatis之间的区别

#### Mybatis

常用标签，[常用注解](https://github.com/9pound/Accumulate/blob/master/mybatis/Mybatis%20%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3.md)

[动态SQL](https://github.com/9pound/Accumulate/blob/master/mybatis/%E5%8A%A8%E6%80%81SQL.md)

如何重数据库中返回自增ID

[mapper接口和xml文件是如何关联的？接口中的方法和xml文件中的sql语句是如何关联的？不同XML文件中id是否可以重复？](https://github.com/9pound/Accumulate/blob/master/mybatis/mapper%E6%8E%A5%E5%8F%A3%E5%92%8Cxml%E6%96%87%E4%BB%B6%E6%98%AF%E5%A6%82%E4%BD%95%E5%85%B3%E8%81%94%E7%9A%84%EF%BC%9F%E6%8E%A5%E5%8F%A3%E4%B8%AD%E7%9A%84%E6%96%B9%E6%B3%95%E5%92%8Cxml%E6%96%87%E4%BB%B6%E4%B8%AD%E7%9A%84sql%E8%AF%AD%E5%8F%A5%E6%98%AF%E5%A6%82%E4%BD%95%E5%85%B3%E8%81%94%E7%9A%84%EF%BC%9F.md)

接口中参数与Sql语句中的参数如何绑定

[数据库表字段和Java类属性字段名不匹配如何解决？](https://github.com/9pound/Accumulate/blob/master/mybatis/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A1%A8%E5%AD%97%E6%AE%B5%E5%92%8CJava%E7%B1%BB%E5%B1%9E%E6%80%A7%E5%AD%97%E6%AE%B5%E5%90%8D%E4%B8%8D%E5%8C%B9%E9%85%8D%E5%A6%82%E4%BD%95%E8%A7%A3%E5%86%B3%EF%BC%9F.md)

#{}与${}的区别？

动态Sql的原理？

动态代理的原理？

[Mybatis延迟加载](https://github.com/9pound/Accumulate/blob/master/mybatis/%E5%BB%B6%E8%BF%9F%E5%8A%A0%E8%BD%BD.md)

[一对一、一对多映射如何实现？](https://github.com/9pound/Accumulate/blob/master/mybatis/%E6%98%A0%E5%B0%84.md)

[鉴别器映射](https://github.com/9pound/Accumulate/blob/master/mybatis/%E9%89%B4%E5%88%AB%E5%99%A8%E6%98%A0%E5%B0%84.md)

[二级缓存](https://github.com/9pound/Accumulate/blob/master/mybatis/%E4%BA%8C%E7%BA%A7%E7%BC%93%E5%AD%98.md)

#### Spring

什么是Spring

资源访问Resource

[核心接口BeanFactory、ApplicationContext、WebApplicationContext](https://github.com/9pound/Accumulate/blob/master/spring/Spring%E6%A0%B8%E5%BF%83%E6%8E%A5%E5%8F%A3.md)

Bean的生命周期14步

IOC

[依赖注入的三种方式](https://github.com/9pound/Accumulate/blob/master/spring/IOC%E7%B1%BB%E5%9E%8B.md)

[自动装配的类型](https://github.com/9pound/Accumulate/blob/master/spring/%E8%87%AA%E5%8A%A8%E8%A3%85%E9%85%8D%E7%9A%84%E7%B1%BB%E5%9E%8B.md)

[Bean的作用域](https://github.com/9pound/Accumulate/blob/master/spring/Bean%E7%9A%84%E4%BD%9C%E7%94%A8%E5%9F%9F.md)

实现Spring的IOC

AOP

[Spring Aop 和AspectJ Aop 有什么区别？](https://github.com/9pound/Accumulate/blob/master/spring/Spring%20Aop%20%E5%92%8CAspectJ%20Aop%20%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB%EF%BC%9F.md)

[JDK动态代理与CGLib代理有什么区别？](https://github.com/9pound/Accumulate/blob/master/spring/JDK%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E4%B8%8ECGLib%E4%BB%A3%E7%90%86%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB%EF%BC%9F.md)

[Spring事务](https://github.com/9pound/Accumulate/blob/master/spring/Spring%E4%BA%8B%E5%8A%A1.md)

数据库事务的特性ACID

[并发问题（五种读）](https://github.com/9pound/Accumulate/blob/master/spring/%E4%BA%94%E7%A7%8D%E6%95%B0%E6%8D%AE%E5%BA%93%E5%B9%B6%E5%8F%91%E9%97%AE%E9%A2%98.md)

[事务的隔离级别](https://github.com/9pound/Accumulate/blob/master/spring/%E4%BA%8B%E5%8A%A1%E7%9A%84%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB.md)

Spring如何使用ThreadLocal解决线程安全问题？

- 一般情况下，从接受请求到返回响应所经过的所有程序调用都属于同一个线程

- ThreadLocal：为不同的事务线程提供独立的资源副本


事务管理器

[事务的传播行为](https://github.com/9pound/Accumulate/blob/master/spring/%E4%BA%8B%E5%8A%A1%E7%9A%84%E4%BC%A0%E6%92%AD%E8%A1%8C%E4%B8%BA.md)

[Spring如何进行事务管理？](https://github.com/9pound/Accumulate/blob/master/spring/Spring%E5%A6%82%E4%BD%95%E8%BF%9B%E8%A1%8C%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86%EF%BC%9F.md)

@Transactional注解

Spring中用到的设计模式

#### Spring MVC

什么是MVC模式、简单谈谈你对 MVC 的理解

SpringMVC工作原理（7步）

参数绑定

说说你对自定义数据类型转换器的理解。

 Spring MVC 怎么样设定重定向和转发的？

@Contorller与@RestController 的区别

@ModelAttribute 注解应该如何使用？

@ResponseEntity

@PathVariable@MatrixVariable

@RequestParam

@CookieValue

@RequestHeader

参数绑定到对象、ServletAPI作为入参、IO对象做入参

HttpMessageConverter

文件上传

静态资源处理

异常处理





如何解决 POST 请求和 GET 请求的中文乱码问题？

#### Spring Boot

[Spring Boot 2.0、起步依赖、自动配置](https://github.com/9pound/Accumulate/blob/master/spring-boot/SpringBoot.md)

[@SpringBootApplication 注解](https://github.com/9pound/Accumulate/blob/master/spring-boot/%40SpringBootApplication%E6%B3%A8%E8%A7%A3.md)

[自动配置的原理](https://github.com/9pound/Accumulate/blob/master/spring-boot/%E8%87%AA%E5%8A%A8%E9%85%8D%E7%BD%AE%E7%9A%84%E5%8E%9F%E7%90%86.md)

Spring Boot的starter原理，自己实现一个starter

### Spring Cloud

服务发现与注册：Eureka、Zookeeper、Consul

负载均衡：Feign、Spring Cloud Loadbalance

服务配置：Spring Cloud Config

服务限流与熔断：Hystrix

服务链路追踪：Dapper

服务网关、安全、消息

什么是 Spring Cloud？

Spring Cloud 和 Spring 之间有什么关联关系？

Spring Cloud 实现服务注册和发现的原理是什么？

 Ribbon 和 Feign 有什么区别？

为什么要使用 Spring Cloud 熔断器，它的作用是什么？

什么是 Hystrix？

Eureka 和 ZooKeeper 有哪些区别？

为什么要使用负载均衡？

Spring Cloud 实现服务注册和发现的具体流程是什么？

为什么要使用 Spring Cloud ，它有哪些优势？

谈谈你对微服务的理解。

微服务分别有哪些优点，哪些缺点？

谈谈微服务之间是如何实现通信的。

Spring Boot 如何集成 MyBatis？

Spring Boot 和 Spring Cloud 有哪些区别？

使用 layui 的数据表格组件展示业务数据，后台实体类应该如何定义

JPA 和 Spring Data JPA 是一回事吗？

如果要给项目添加权限管理系统，一般包含哪些需求？

微服务架构的拆分都有哪些原则？

Feign 和 Ribbon+RestTemplate 的区别是什么？

### Spring Security

### RabbitMQ

什么是 rabbitmq、为什么要使用 rabbitmq、使用 rabbitmq 的场景、mq 的优缺点？

如何确保消息正确地发送至 RabbitMQ？ 

如何确保消息接收方消费了消息？

如何避免消息重复投递或重复消费？

消息基于什么传输？

消息如何分发？

消息怎么路由？

如何确保消息不丢失？

RabbitMQ 的集群

### 应用服务器知识

#### JBoss

#### tomcat

#### jetty

#### Weblogic

### 工具

#### git & svn

#### maven & gradle

#### Intellij IDEA

常用插件：Maven Helper 、FindBugs-IDEA、阿里巴巴代码规约检测、GsonFormat

Lombok plugin、.ignore、Mybatis plugin

## 四、 高级篇

### 新技术

#### Java 8

lambda表达式、Stream API、时间API

#### Java 9

Jigsaw、Jshell、Reactive Streams

#### Java 10

局部变量类型推断、G1的并行Full GC、ThreadLocal握手机制

#### Java 11

ZGC、Epsilon、增强var、

#### Spring 5

响应式编程

#### Spring Boot 2.0

### http/2

### http/3

### 性能优化

使用单例、使用Future模式、使用线程池、选择就绪、减少上下文切换、减少锁粒度、数据压缩、结果缓存

### 线上问题分析

#### dump获取

线程Dump、内存Dump、gc情况

#### dump分析

分析死锁、分析内存泄露

#### dump分析及获取工具

jstack、jstat、jmap、jhat、Arthas

#### 自己编写各种outofmemory，stackoverflow程序

HeapOutOfMemory、 Young OutOfMemory、MethodArea OutOfMemory、ConstantPool OutOfMemory、DirectMemory OutOfMemory、Stack OutOfMemory Stack OverFlow

#### Arthas

jvm相关、class/classloader相关、monitor/watch/trace相关、

options、管道、后台异步任务

文档：https://alibaba.github.io/arthas/advanced-use.html

#### 常见问题解决思路

内存溢出、线程死锁、类加载冲突

#### 使用工具尝试解决以下问题，并写下总结

当一个Java程序响应很慢时如何查找问题、

当一个Java程序频繁FullGC时如何解决问题、

如何查看垃圾回收日志、

当一个Java应用发生OutOfMemory时该如何解决、

如何判断是否出现死锁、

如何判断是否存在内存泄露

使用Arthas快速排查Spring Boot应用404/401问题

使用Arthas排查线上应用日志打满问题

利用Arthas排查Spring Boot应用NoSuchMethodError

### 编译原理知识

#### 编译与反编译

#### Java代码的编译与反编译

#### Java的反编译工具

javap 、jad 、CRF

#### 即时编译器

#### 词法分析，语法分析（LL算法，递归下降算法，LR算法），语义分析，运行时环境，中间代码，代码生成，代码优化

### 操作系统知识

#### Linux的常用命令

#### 进程间通信

竞争条件

临界区

生产者消费者问题、哲学家就餐问题、读者写者问题

信号量

互斥量

管程

消息传递

屏障

#### 死锁

死锁的条件

鸵鸟算法

死锁的检测与恢复

死锁的避免、银行家算法

死锁的预防

#### 缓冲区溢出

#### 分段和分页

#### 虚拟内存与主存

#### 虚拟内存管理

#### 换页算法

### 数据库知识



##### 连接

内连接，左连接，右连接

#### MySQL

##### MySql 执行引擎  

##### MySQL 执行计划

如何查看执行计划，如何根据执行计划进行SQL优化？

一条SQL语句在MySQL中如何执行？

一条SQL语句执行得很慢的原因有哪些？

##### 索引

Hash索引、B树索引（B+树、和B树、R树）

普通索引、唯一索引

覆盖索引、最左前缀原则、索引下推

##### SQL优化

##### 数据库事务和隔离级别

事务的隔离级别、事务能不能实现锁的功能

##### MVCC

##### 数据库锁

行锁、表锁、使用数据库锁实现乐观锁？

InnoDB锁算法

##### 数据库主备搭建

#### binlog

#### redolog

#### 内存数据库

h2

#### 分库分表

#### 读写分离

### NOSql数据库

#### redis

数据结构（常用命令）9种

持久化（RDB&AOF）

主从复制

事务（MULTI&EXEC）

高可用（主从、哨兵、集群）

应用（分布式锁&延时队列)

[参考](https://blog.csdn.net/Design407/article/details/103242874?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight)

ElasticSearch



[参考](https://zhuanlan.zhihu.com/p/102500311)

#### 分别使用数据库锁、NoSql实现分布式锁

#### 性能调优

#### 数据库连接池

### 数据结构与算法知识

#### 简单的数据结构

栈、队列、链表、数组、哈希表、

栈和队列的相同和不同之处

栈通常采用的两种存储结构

#### 树

二叉树、字典树、平衡树、排序树、B树、B+树、R树、多路树、红黑树

#### 堆

大根堆、小根堆

#### 图

有向图、无向图、拓扑

#### 排序算法

稳定的排序：冒泡排序、插入排序、鸡尾酒排序、桶排序、计数排序、归并排序、原地归并排序、二叉排序树排序、鸽巢排序、基数排序、侏儒排序、图书馆排序、块排序

不稳定的排序：选择排序、希尔排序、Clover排序算法、梳排序、堆排序、平滑排序、快速排序、内省排序、耐心排序

各种排序算法和时间复杂度

#### 深度优先和广度优先搜索

#### 全排列、贪心算法、KMP算法、hash算法

#### 海量数据处理

分治，hash映射，堆排序，双层桶划分，Bloom Filter，bitmap，数据库索引，mapreduce等。

#### 两个栈实现队列，和两个队列实现栈

### 大数据知识

#### Zookeeper

基本概念、常见用法

#### Solr，Lucene，ElasticSearch

在linux上部署solr，solrcloud，，新增、删除、查询索引

#### Storm，流式计算，了解Spark，S4

在linux上部署storm，用zookeeper做协调，运行storm hello world，local和remote模式运行调试storm topology。

#### Hadoop，离线计算

HDFS、MapReduce

#### 分布式日志收集flume，kafka，logstash

#### 数据挖掘，mahout

### 网络安全知识

#### XSS

XSS的防御

#### CSRF

#### 注入攻击

SQL注入、XML注入、CRLF注入

#### 文件上传漏洞

#### 加密与解密

对称加密、非对称加密、哈希算法、加盐哈希算法

MD5，SHA1、DES、AES、RSA、DSA

彩虹表

#### DDOS攻击

DOS攻击、DDOS攻击

memcached为什么可以导致DDos攻击、什么是反射型DDoS

如何通过Hash碰撞进行DOS攻击

#### SSL、TLS，HTTPS

#### 用openssl签一个证书部署到apache或nginx

## 五、架构篇

### 分布式

CAP和BASE理论

数据一致性、服务治理、服务降级

#### 分布式事务

2PC、3PC、CAP、BASE、 可靠消息最终一致性、最大努力通知、TCC

#### Dubbo

服务注册、服务发现，服务治理

http://dubbo.apache.org/zh-cn/

#### 分布式数据库

怎样打造一个分布式数据库、什么时候需要分布式数据库、mycat、otter、HBase

#### 分布式文件系统

mfs、fastdfs

#### 分布式缓存

缓存一致性、缓存命中率、缓存冗余

#### 限流降级

Hystrix、Sentinal

#### 算法

共识算法、Raft协议、Paxos 算法与 Raft 算法、拜占庭问题与算法

2PC、3PC

### 微服务

SOA、康威定律

#### ServiceMesh

sidecar

#### Docker & Kubernets

#### Spring Boot

#### Spring Cloud

### 高并发

#### 分库分表

#### CDN技术

#### 消息队列

ActiveMQ

### 监控

#### 监控什么

CPU、内存、磁盘I/O、网络I/O等

#### 监控手段

进程监控、语义监控、机器资源监控、数据波动

#### 监控数据采集

日志、埋点

#### Dapper

### 负载均衡

tomcat负载均衡、Nginx负载均衡

四层负载均衡、七层负载均衡

### DNS

DNS原理、DNS的设计

### CDN

数据一致性

## 六、 扩展篇

### 云计算

IaaS、SaaS、PaaS、虚拟化技术、openstack、Serverlsess

### 搜索引擎

Solr、Lucene、Nutch、Elasticsearch

### 权限管理

Shiro

### 区块链

哈希算法、Merkle树、公钥密码算法、共识算法、Raft协议、Paxos 算法与 Raft 算法、拜占庭问题与算法、消息认证码与数字签名

#### 比特币

挖矿、共识机制、闪电网络、侧链、热点问题、分叉

#### 以太坊

#### 超级账本

### 人工智能

数学基础、机器学习、人工神经网络、深度学习、应用场景。

#### 常用框架

TensorFlow、DeepLearning4J

### IoT

### 量子计算

### AR & VR

### 其他语言

Groovy、Python、Go、NodeJs、Swift、Rus