# FAQ





### 生产者

Api 

KafkaProducer

- topic
- partition
- key
- value

ProducerRecord



分区方法、序列化器、

二进制连接协议





消息是怎么重试的？ 

生产者怎么重试？

消费者怎么重试？



![image-20210825170845590](E:\Accumulate\kafka\FAQ.assets\image-20210825170845590.png)



![image-20210825170900303](E:\Accumulate\kafka\FAQ.assets\image-20210825170900303.png)



1、Kafka是什么？
2、partition的数据文件（offffset，MessageSize，data）
3、数据文件分段 segment（顺序读写、分段命令、二分查找）
4、负载均衡（partition会均衡分布到不同broker上）
5、批量发送
6、压缩（GZIP或Snappy）
7、消费者设计
8、Consumer Group
9、如何获取topic主题的列表
10、生产者和消费者的命令行是什么？
11、consumer是推还是拉？
12、讲讲kafka维护消费状态跟踪的方法
13、讲一下主从同步。
14、为什么需要消息系统，mysql 不能满足需求吗？
15、Zookeeper对于Kafka的作用是什么？
16、Kafka判断一个节点是否还活着有那两个条件？
17、Kafka与传统MQ消息系统之间有三个关键区别
18、讲一讲kafka的ack的三种机制
19、消费者如何不自动提交偏移量，由应用提交？
20、消费者故障，出现活锁问题如何解决？
21、如何控制消费的位置？
22、kafka分布式（不是单机）的情况下，如何保证消息的顺序消费？
23、kafka的高可用机制是什么？
24、kafka如何减少数据丢失？
25、kafka如何不消费重复数据？比如扣款，我们不能重复的扣？