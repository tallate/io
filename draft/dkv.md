设计


# dkv(Decentralized-Key-Value)

存储是架构中最难的部分，从ACID到BASE，从高性能到高可用，现在的互联网项目大多是数据密集型的，架构的设计总是要围绕着存储来进行。
现今大部分架构里的存储一般都是中心化的，就算要分库分表，也要深入理解业务，按业务进行拆分或按id进行hash等，没有办法做到“非常自由”的伸缩，而去中心化就是对这种现状的挑战。
总之，这是我在分布式领域里面可以想到的最大的挑战，我们先来梳理一下分布式系统的基础知识，然后分析一下数据库技术的现状。


## 一、分布式系统原理
1. [走向分布式](http://dcaoyuan.github.io/papers/pdfs/Scalability.pdf)


## 二、存储发展现状
### 架构发展
架构中最难的方面是存储，架构受存储的制约，反过来，我们也可以从架构中看到存储技术的演进：
1. [网站架构相关PPT、文章整理（更新于2009-7-15）](http://www.blogjava.net/BlueDavy/archive/2009/04/28/267970.html)
1. [从零开始搭建创业公司后台技术栈](http://ju.outofmemory.cn/entry/351897)

### 键值对数据库（KV Store）
本地缓存（Guava、Chronicle-Map、ehcache）
Memcached
Redis
* [面试题：“选redis还是memcache”](https://juejin.im/post/5cd5174d6fb9a0324e4a53b0)
Cassandra
RocksDB
Titan
* [Titan 的设计与实现](https://www.jianshu.com/p/7d115c8ecb1e)

应用（名称解析 / 服务注册 / 缓存 / 定时器elasticjob / session）
中心化（redis、codis） 
协调协议（Paxos、Zab、Raft、sofa-jraft、gossip）
时间协调
初衷（原中心化的缓存不好管理，其实可以选举出一个中心节点来加载数据，然后同步到其他节点。减少使用本地缓存时单个服务器内存压力）
数据分片（过大的value被切片，并行读提高获取时的速度）

如何使用go语言实现一个分布式缓存。
[hashicorp/memberlist](https://github.com/hashicorp/memberlist)
基于gossip的容错集群成员管理。
[stathat/consistent](https://github.com/stathat/consistent)
使用一致性哈希算法实现数据分片。


### 文档数据库
MongoDB
Elasticsearch
[valeriansaliou/sonic](https://github.com/valeriansaliou/sonic)

### 列数据库
BigTable
Hbase

### 图数据库
Neo4j
FlockDB

### 关系型数据库
分布式事务-中间件层：sharding-jdbc、mycat、mysql-proxy
分布式事务-业务层：atomikos、Fescar、tcc-transaction、ByteTCC
分布式事务-协议层：Percolator、XA
分布式数据库：RadonDB、BigTable、RocksDB、F1、Spanner、CockroachDB、TiDB
SQL解释器（Calcite）
索引：cpp-btree（Google）、SlimTrie
sql优化原理
锁：原理、排查
集群 读写分离
内存数据库：VoltDB

Bluzelle（声称是去中心化数据库，但是其技术细节并未公布，可能是挂羊头买狗肉）
1. [去中心化数据库：传统IT与区块链的未来融合形式](http://www.ymcall.com/artinfo/949446562686071991.html)
1. [Bluzelle-区块链上的甲骨文](https://www.jianshu.com/p/4e0c7ebceb7c)

除了 Redis 这些常见的缓存中间件外，一些大数据相关的内存数据管理框架也能承担分布式缓存的职责，虽然很多情况下是“杀鸡用牛刀”、徒增复杂度，但是其中很多思路是可以学习的。
1. [github - apache/ignite](https://github.com/apache/ignite)
1. [github - apache/arrow](https://github.com/apache/arrow)

### 文件系统
HDFS
1. [去中心化的分布式存储模型](https://www.ixueshu.com/download/bdae7db2d3cee26e14a4dc030e7d94c3.html)

p2p协议（bt伪去中心化、ipfs去中心化、Sia、Storj）
版本控制（Git）


## 参考




块存储


分布式文件系统
HDFS


对象存储


键值对数据库（KV Store）
Redis
Memcached
Cassandra
去中心化键值对存储
应用（名称解析 / 服务注册 / 缓存 / 定时器elasticjob / session）
中心化（redis、codis） p2p协议（bt伪去中心化、ipfs去中心化、Sia、Storj）
版本控制（Git） 协调协议（Paxos、Zab、Raft、sofa-jraft、gossip） 时间协调 初衷（原中心化的缓存不好管理，其实可以选举出一个中心节点来加载数据，然后同步到其他节点。减少使用本地缓存时单个服务器内存压力） 数据分片（过大的value被切片，并行读提高获取时的速度） 本地缓存（Guava、Chronicle-Map）

文档数据库
MongoDB

列数据库
BigTable
Hbase

图数据库
Neo4j
FlockDB

去中心化分布式数据库
分布式事务-中间件层：sharding-jdbc、mycat、mysql-proxy
分布式事务-业务层：atomikos、Fescar、tcc-transaction、ByteTCC
分布式事务-协议层：Percolator、XA
分布式数据库：TiDB、BigTable、RocksDB、F1、Scanner 
SQL解释器（Calcite）
索引：cpp-btree（Google）、SlimTrie
sql优化原理
锁：原理、排查
集群 读写分离


## 参考
### 存储相关概念
1. [块存储、文件存储、对象存储这三者和分布式文件存储系统的本质区别](https://blog.csdn.net/zds05/article/details/79494870)
1. [DB-Engines](db-engines.com)
数据库排名
### 键值对存储
1. [分布式键值对存储系统的设计与实现](https://m.doc88.com/p-8962526015056.html)
### 数据库
1. [Readings in Database Systems](http://www.redbook.io/index.html)
第5版是最新的，这一系列包含了数据管理的一些经典和前沿研究。
### 去中心化存储
1. 《区块链核心算法解析》
1. [去中心化的分布式存储模型](https://www.ixueshu.com/download/bdae7db2d3cee26e14a4dc030e7d94c3.html)


