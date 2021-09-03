# Netty组件

基于JavaNIO的异步的和事件驱动的实现，保证了高负载情况下应用程序性能的最大化和可伸缩性

## Channel

本质：就是封装了Socket，提供基本的IO操作，

作用：降低了Socket的使用复杂性

实现类

- EmbeddedChannel
- LocalServerChannel
- NioDatagramChannel
- NioSctpChannel
- NioSocketChannel

## EventLoop接口

用于处理连接生命周期中所发生的事件。

- 一个EventLoopGroup包含一个或多个EventLoop
- 一个EventLoop在它的生命周期内只和一个Thread绑定
- 所有由EventLoop处理的IO事件都将在它专有的Thread上被处理
- 一个Channel在它的生命周期内只注册于一个EventLoop中；
- 一个EventLoop可能会被分配给一个或多个Channel

作用：一个给定的Channel的IO操作都是由相同的Thread执行的，消除了对于同步的需要

## EventLoopGroup

EventLoopGroup负责为每个新创建的Channel分配一个EventLoop（一般顺序循环分配）

## ChannelFuture接口：

netty中所有的IO操作都是异步的，ChannelFuture用于在之后的某个时间点确定结果。

## ChannelHandler接口：

本质：封装了事件处理的业务逻辑、负责接收并响应事件的通知。

netty以适配器的形式提供了大量默认的ChannelHandler实现

- ChannelHandlerAdapter
- ChannelInBoundHandlerAdapter
- ChannelOutBoundHandlerAdapter
- ChannelDuplexHandler

## ChannelPipeline接口：

**本质**：ChannelHandler的实例链的容器、（ChannelHandler 的双向链表）

**性质**：

- ChannelHandler的执行顺序就是它们被添加的顺序
- 当ChannelHandler被添加到ChannelPipleline时，它将会被分配一个ChannelHandlerContext，其代表了ChannelHandler和ChannelPipeline之间的绑定

**ChannelPipeline安装ChannelHandler的过程**

- 一个ChannelInitializer的实现被注册到SeverbootStrap 中
- 当ChannelInitializer.initChannel方法被调用时，ChannelInitializer将在ChannelPipeline中安装一组自定义的ChannelHandler
- ChannelInitializer将它自己冲ChannelPipeline中移除

**ChannelHandlerContext**：

代表了Channelhanler和ChanelPipeline之间的绑定

他会被传递给Channelhandler的所有

**适配器类**：提供了定义在对应接口中的所有方法的默认实现

- ChannelHandlerAdapter
- ChannelInboundHandlerAdapter
- ChannelOutboundHandlerAdapter
- ChanelDuplexHandler

**Netty中两种发消息的方式：**

- 直接写到Channel中，（消息从ChannelPipeline的尾端开始流动）
- 写到与ChannelHandler相关联的ChannelHandlerContext对象中。（消息从ChannelPipeline中的下一个ChannelHandler开始流动）

## 编码器和解码器

本质：ChannelHandler的子类

**编码器**：出站消息会被编码，从当前格式被编码为字节

**解码器**：入站消息会被解码，从字节转换为另一种格式

**SimpleChannelInboundHandler**：一般是扩展这个类，来接受解码的消息，并执行响应的业务逻辑。

所有由Netty提供的编码器、解码器适配器类都实现了ChannelOutboundHandler 或者 ChannelInboundHandler接口

## 引导类

**本质**：网络配置的容器，将一个进程绑定到某个指定的端口，或者将一个进程连接到另一个运行在某个指定主机的指定端口上的进程

**引导的类型有两种**：客户端，服务端

​	Bootstrap 和 ServerBootstrap

**区别**：

- 客户端需要绑定端口，监听连接。服务端建立到一个或者多个进程的连接

- 引导客户端只需要一个EventLoopGroup，而引导一个服务端则需要两个（可以是同一个实例）