


## mysql

开启binlog，ROW模式
[mysqld]
log-bin=/home/worker/mysql/mysql-bin # 开启 binlog
log_bin=1
binlog-format=ROW # 选择 ROW 模式
server_id=1 # 配置 MySQL replaction 需要定义，不要和 canal 的 slaveId 重复
创建用户
CREATE USER "canal"@"%" IDENTIFIED BY "9canal_Benmu";
-- GRANT SELECT, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'canal'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'canal'@'%' ;
FLUSH PRIVILEGES;
canal部署

canal-srv
由于数据和资源先考虑canal单实力，但要修改多模块
https://github.com/alibaba/canal/wiki/QuickStart


虚机账号密码：root    vTr5bjkBVj9l
canal-client
示例代码，要注意code逻辑合理性
https://github.com/alibaba/canal/wiki/ClientAPI
canal-多model


## canal
原理：模拟了mysql的slave
binlog记录模式：模式把update记下来、row行级模式记录数据快照，canal是row模式
canal配置数据库：canal.properties中加描述并新建一个{库名}/instance.properties，位点binlog中的，
canal客户端配置：配置以客户端为准，可以配数据库和表
单机模式：直连
集群模式：以第一台启动的为准，使用ZooKeeper注册服务地址
dev不能改成prod，因为和线上的是直连的





