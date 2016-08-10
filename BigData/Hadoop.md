

# Hadoop Family

## Hadoop

对于 Hadoop 的集群来讲，可以分成两大类角色：**Master**和**Salve**。一个 HDFS 集群是由一个NameNode 和若干个 DataNode 组成的。其中 NameNode 作为主服务器，管理文件系统的命名空间和客户端对文件系统的访问操作；集群中的 DataNode 管理存储的数据。

MapReduce 框架是由一个单独运行在主节点上的 JobTracker 和运行在每个从节点的 TaskTracker 共同组成的。主节点负责调度构成一个作业的所有任务，这些任务分布在不同的从节点上。主节点监控它们的执行情况，并且重新执行之前的失败任务；从节点仅负责由主节点指派的任务。当一个 Job 被提交时，JobTracker接收到提交作业和配置信息之后，就会将配置信息等分发给从节点，同时调度任务并监控 TaskTracker 的执行。

从上面的介绍可以看出，HDFS 和 MapReduce 共同组成了 Hadoop 分布式系统体系结构的核心。HDFS 在集群上实现分布式文件系统，MapReduce 在集群上实现了分布式计算和任务处理。HDFS 在 MapReduce 任务处理过程中提供了文件操作和存储等支持，MapReduce 在 HDFS 的基础上实现了任务的分发、跟踪、执行等工作，并收集结果，二者相互作用，完成了 Hadoop 分布式集群的主要任务。

## [Apache Sqoop](http://sqoop.apache.org/)

是一个用来将Hadoop和关系型数据库中的数据相互转移的工具，可以将一个关系型数据库（MySQL ,Oracle ,Postgres等）中的数据导进到Hadoop的HDFS中，也可以将HDFS的数据导进到关系型数据库中。
    

## [Apache Avro](http://avro.apache.org/)

是一个数据序列化系统，设计用于支持数据密集型，大批量数据交换的应用。有点类似Google的protobuf和Facebook的thrift。avro用来做以后hadoop的RPC，使hadoop的RPC模块通信速度更快、数据结构更紧凑。



# Reference

- [Hadoop 家族学习路线图](http://blog.fens.me/hadoop-family-roadmap/)
- [SQL与NoSQL，数据桥梁Sqoop](http://www.jianshu.com/p/7fcb24949637)


