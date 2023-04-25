# ZAB协议

为分布式协调服务ZooKeeper专门设计的一种支持崩溃恢复的原子广播协议





主备模式

单一主进程

全局变更序列



事务请求的处理方式





## 两种基本模式

### 消息广播

何时进入

何时退出

#### 原理 

- 使用一个原子广播协议，类似于二阶段提交
- 使用tcp通信



#### 工作过程

- 生成Proposal 并分配全局单调递增的唯一ID(ZXID又称为事务ID)
- 对每个事务请求生成进行广播
- leader 为每个follower分配一个单独的队列，按FIFO发送
- follower接受到事务proposal，以事务日志写入本地磁盘
- 写入成功反馈给Leader一个 ack 响应
- Leader 接收到超过半数Follower的Ack，广播一个commit 消息、自身提交事务
- Follower 接收到Commit 事务后 提交事务



### 崩溃恢复

何时进入

- Leader服务器崩溃
- 网络原因，Leader服务器失去了与过半Follower的联系

何时退出

 

工作过程

Leader 广播 proposal 之后立刻挂了 - 丢弃提案

Leader 广播 commit 之前挂了- 提交提案



#### Leader选举算法

- 确保提交已被Leader提交的事务Proposal
- 丢弃已经被跳过的事务Proposal



#### 数据同步过程

选举之后，开始工作之前







ZXID64位数据，

低32位：单调递增计数器，

高32位: 递增epoch 值



**无法处理leader服务器崩溃带来的不一致问题，如何解决？**

**不同于二阶段提交的地方？**



### 数据恢复模式

