# kafka 生产者

#### 场景：

- 是否每个消息都很总要？
- 是否允许丢失一部分消息？
- 偶尔出现重复消息是否可以接收？
- 是否有严格的延迟和吞吐量要求？
- 

kafkaProducer

ProducerRecords



分区方法

自定义

序列化器

自定义



#### 发消息的步骤：

1、创建ProducerRecords(主题，内容，键，分区)

2、数据被传给分区器，如果指定了分区，直接把指定的分区返回，如果没有指定分区，那么分区会根据键来选择一个分区

3、记录被添加到一个记录批次里，这个批次里的所有消息都会被发送到相同的主题和分区上

4、服务器接收消息返回一个响应，如果成功写入kafka，返回一个RecordMetaData对象，它包含了主题，分区信息，和在分区里的偏移量。如果写入失败，则会返回一个错误，生产者接受到错误之后会尝试重新发送消息，几次之后如果还是失败，就返回错误信息



示例代码



```java
/* 
    生产者的三个必选属性
    bootstrap.servers
    key.serializer
    value.serializer
*/
private Properties kafkaProps = new Properties();

producer = new KafkaProducer<String,String>(kafkaprops);


```



#### 发消息的方式：

- 发送并忘记
  - 把消息发送给服务器，但是并不关心它是否正常到达
- 同步发送
  - 用send（）发送消息，返回一个Future对象，调用get方法进行等待
- 异步发送
  - 调用send方法并指定一个回调函数，服务器在返回响应时调用该函数



#### 常用参数：

- acks：制定了必须要有多少个分区副本收到消息，生产者才会认为消息写入是成功的
  - acks = 0,生产者在成功消息之前不会等待来自服务器的响应，如果当中出现问题，导致服务器没有接受到。
  - acks = 1,只要集群的首领节点收到消息，生产者就会收到一个来自服务器的成功响应。
  - acks=all，只有当所有参与节点复制的节点全部收到消息时，生产者才会收到一个来自服务器的成功响应。
- retries：生产者可以重发消息的次数，默认情况下每次重试之间等待100 毫秒
- 



[SpringBoot集成kafka全面实战_Felix-CSDN博客](https://blog.csdn.net/yuanlong122716/article/details/105160545/)