# cluster

目的：提高集群的容错性和可扩展性，要达到两个目标
1. 当集群当中的一个节点down 掉，还能不能正常对外提供服务
2.
 

**注意节点情况**
 
1. 每个clusterNode 都存储整个集群当中的部分数据，而不是全部，在这里要跟主从复制区分开来，

2. 主从复制是主数据库和从数据库拥有完整的数据库
 
 
# 一直性hash算法
  
传统一直性hash算法存在的问题，缓存部分失效，导致数据迁移部分失效
 

# slot槽

1. Redis Cluster中，Sharding采用slot(槽)的概念，一共分成16384个槽，每次槽采用一个位表示, bitmap

2. sharding思路。对于每个进入Redis的键值对，根据key进行散列，分配到这16384个slot中的某一个中。

3. 然后每个cluster node 负责一些slot槽， 槽的<key,value> 就存储在该节点上面

4. 集群当中的每个节点可以处理0个或最多16384个槽，因此一个集群最多可以拥有16384个节点
 
 
# cluster模式存在的缺点问题

1. 因为每个节点都只有存储部分信息，如果发生故障，这部分数据不见了怎么办？

2. 所以我们一般都是讲cluster模式和主从复制搭配使用，每个节点采用主从复制的模式，主节点崩溃了，那么从数据库和主节点数据是一样的，所有还是可以对外正常提供服务的基本情况。





