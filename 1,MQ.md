rocetmq   独有的事务处理能力： 弱事务，无法回滚，最终一致性







![image-20191213115830751](images/image-20191213115830751.png)



为什么activeMQ有较低概率丢失数据？

因为是异步的处理机制，并且没有持久化的机制。在主从架构下，master收到消息直接返回，有可能正在异步同步化给slave的时候宕机了，导致消息丢失。另外没有持久化的机制，未落盘的情况下宕机了。



主从架构的，异步落盘的，就有可能会发生数据丢失。

CAP中AP模型会有数据丢失的问题



每秒1万条消息



![image-20191213142211454](images/image-20191213142211454.png)

图中都是master主机





每隔30秒向nameserve发送心跳。

如果心跳超时怎么办？nameserve每隔10秒nameserve向下扫描broker，这个时间是写死的，若broker2分钟没有响应。那么认为broker已经挂了。



主机同步从机持久化，保证消息不丢失。

  



为什么搞多个队列？

因为队列每一时刻只能有一个消费者。
