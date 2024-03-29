# 面试题FAQ



## 1、Netty 是什么？

netty是一款异步的、事件驱动的、用来快速开发高性能的网络应用程序的框架

异步：异步方法会立即返回，并且在它完成时，会直接或者在稍后的某个时间点通知用户

​			Socket 编程是一个连接，一个线程。在从socket中读取数据的时候，这一步是阻塞的。而netty基于NIO，基于selector，可以监听多个连接上的事件。

事件驱动

## 2、Netty的特点？

易用

高性能

零拷贝

## 3、BIO、NIO和AIO的区别？

1）Java BIO (blocking I/O)：同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善；
2）Java NIO (non-blocking I/O)： 同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。

Java AIO(NIO.2) ： 异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理。



- BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解。
- NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持。
- AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支



阻塞和非阻塞网络操作之间的区别？

异步I/O 在高容量、高性能的网络编程中的优势？

异步模型的底层机制？

Netty 中有哪种重要组件？

Netty的线程模型？

什么是 Netty 的零拷贝？

Netty 发送消息有几种方式？

**什么是 Reactor 模型**

**了解哪几种序列化协议**

**Netty怎样实现零拷贝**

讲讲Netty的特点？

NIO的组成是什么？

如何使用 Java NIO 搭建简单的客户端与服务端实现网络通讯？

如何使用 Netty 搭建简单的客户端与服务端实现网络通讯？

讲讲Netty 底层操作与 Java NIO 操作对应关系？

Channel 与 Socket是什么关系，Channel 与 EventLoop是什么关系，Channel 与 ChannelPipeline是什么关系？

EventLoop与EventLoopGroup 是什么关系？

说说Netty 中几个重要的对象是什么，它们之间的关系是什么？

Netty 的线程模型是什么？

## TCP 粘包/拆包的原因及解决方法？

## 13.默认情况 Netty 起多少线程？何时启动？

## 14.了解哪几种序列化协议？









Socket IO是比较重要的一块，要搞懂的是阻塞/非阻塞的区别、同步/异步的区别，借此理解阻塞IO、非阻塞IO、多路复用IO、异步IO这四种IO模型，Socket IO如何和这四种模型相关联。这是基本一些的，深入一些的话，就会问NIO的原理、NIO属于哪种IO模型、NIO的三大组成等等，这有些难，当时我也是研究了很久才搞懂NIO。提一句，**NIO并不是严格意义上的非阻塞IO而应该属于多路复用IO**，面试回答的时候要注意这个细节，讲到NIO会阻塞在Selector的select方法上会增加面试官对你的好感。



参考

[2020 Netty面试题大全_baidu_37366055的博客-CSDN博客_netty面试题](https://blog.csdn.net/baidu_37366055/article/details/104893106)

