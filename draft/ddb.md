# Decentralized-


分布式文件系统
HDFS
1. [去中心化的分布式存储模型](https://www.ixueshu.com/download/bdae7db2d3cee26e14a4dc030e7d94c3.html)

键值对数据库（KV Store）
Redis
Memcached
Cassandra
RocksDB
Titan [Titan 的设计与实现](https://www.jianshu.com/p/7d115c8ecb1e)
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

