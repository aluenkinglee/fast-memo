# ZooKeeper

## 简介

https://zookeeper.apache.org/doc/r3.1.2/zookeeperProgrammers.html

ZooKeeper（动物园管理员），顾名思义，是用来管理Hadoop（大象）、Hive（蜜蜂）、Pig（小猪）的管理员，同时Apache HBase、Apache Solr、LinkedIn Sensei等众多项目中都采用了ZooKeeper。

ZooKeeper曾是Hadoop的正式子项目，后发展成为Apache顶级项目，与Hadoop密切相关但却没有任何依赖。
它是一个针对大型应用提供高可用的数据管理、应用程序协调服务的分布式服务框架，基于对Paxos算法的实现，
使该框架保证了分布式环境中数据的强一致性，提供的功能包括：配置维护、统一命名服务、状态同步服务、集群管理等。

在分布式应用中，由于工程师不能很好地使用锁机制，以及基于消息的协调机制不适合在某些应用中使用，因此需要有一种可靠的、可扩展的、分布式的、可配置的协调机制来统一系统的状态。Zookeeper的目的就在于此。

## 特点

* ZooKeeper的核心是一个精简文件系统，它提供一些简单的操作和一些额外的抽象操作，例如：排序和通知。
* ZooKeeper具有高可用性：ZooKeeper运行在集群上，被设计成具有较高的可用性，因此应用程序可以完全依赖它。ZooKeeper可以帮助系统避免出现单点故障，从而构建一个可靠的应用。


## 重要概念
理解ZooKeeper的一种方法是将其看做一个具有高可用性的文件系统

但这个文件系统中没有文件和目录，而是统一使用节点（node）的概念，称为znode。
znode既可以保存数据（如同文件），也可以保存其他znode（如同目录）。所有的znode构成一个层次化的数据结构，。
* Regular Nodes: 永久有效地节点,除非client显式的删除,否则一直存在
* Ephemeral Nodes: 临时节点,仅在创建该节点client保持连接期间有效,一旦连接丢失,自动删除该节点。并且不能创建子节点。
* Sequence Nodes: 顺序节点,client申请创建该节点时,zk会自动在节点路径末尾添加递增序号,这种类型是实现分布式锁,分布式queue等特殊功能的关键

## 典型使用场景


## 查看日志
Sample
```
// Read snapshot file
java -cp zookeeper-3.4.6.jar:lib/log4j-1.2.16.jar:lib/slf4j-log4j12-1.6.1.jar:lib/slf4j-api-1.6.1.jar org.apache.zookeeper.server.SnapshotFormatter version-2/snapshot.xxx

// Read log file
java -cp zookeeper-3.4.6.jar:lib/slf4j-api-1.6.1.jar org.apache.zookeeper.server.LogFormatter version-2/log.xxx
```
## 配置参数

#### maxClientCnxns
ZooKeeper关于maxClientCnxns参数的官方解释：
> 单个客户端与单台服务器之间的连接数的限制，是ip级别的，默认是60，如果设置为0，那么表明不作任何限制。请注意这个限制的使用范围，仅仅是单台客户端机器与单台ZK服务器之间的连接数限制，不是针对指定客户端IP，也不是ZK集群的连接数限制，也不是单台ZK对所有客户端的连接数限制。

> Limits the number of concurrent connections (at the socket level) that a single client, identified by IP address, may make to a single member of the ZooKeeper ensemble. This is used to prevent certain classes of DoS attacks, including file descriptor exhaustion. The default is 60. Setting this to 0 entirely removes the limit on concurrent connections.

限制的是单个ip上最多能连接zk的个数，而不是总连接个数。

# Misc
http://blog.csdn.net/liuxinghao/article/details/42747625  
http://www.jianshu.com/p/fa204ba67ced  
http://www.jianshu.com/p/7faf4783ee5b  
https://www.ibm.com/developerworks/cn/opensource/os-cn-zookeeper/  

http://www.cnblogs.com/sunddenly/p/4033574.html  
http://www.cnblogs.com/sunddenly/p/4018459.html  
