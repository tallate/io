---
title: MySQL应用总结
categories: 技术点总结
tags:
  - MySQL
  - SQL
  - 事务
abbrlink: 28ae9193
date: 2019-07-10 11:33:18
---


<!-- more -->

## SQL语法
MySQL的基础操作是刚开始接触MySQL必须掌握的，大概包括以下几个部分。
1. MySQL体系结构（模块划分、存储引擎）
1. 数据库基本操作
1. 表基本操作（alter）
1. 数据类型和运算符
1. MySQL函数
1. 查询（select）
1. 插入、更新、删除（insert、update、delete）
1. 用户管理（grant）
1. （Deprecated）存储过程和存储函数（procedure、function）
1. （Deprecated）视图（view）
1. （Deprecated）触发器（trigger）
### json
为了效率，有些开发会将所有字段格式化成json再塞到一个text类型的字段里，虽然业务中确实不会使用这些字段来查询数据，但是很多时候我们会根据其中的某些字段进行数据统计。
1. 查询、过滤
    ```
    {
        "jsonField": "abc"
    }
    
    select JSON_UNQUOTE(JSON_EXTRACT(field_name, '$.jsonField'))
    from table_name
    where JSON_UNQUOTE(JSON_EXTRACT(field_name, '$.jsonField')) = 'abc'
    ```
1. 带数组的情况
    ```
    {
        "jsonArrayField": [
            {
                "field": "a"
            }, {
                "field": "b"
            }
        ]
    }
    -- 获取全部
    select JSON_EXTRACT(JSON_EXTRACT(data, '$.jsonArrayField'), '$[*].field')
    from table_name;
    -- 获取某个下标的数据
    select JSON_EXTRACT(JSON_EXTRACT(data, '$.jsonArrayField'), '$[0].field')
    from table_name;
    ```
### group by
1. 按日期group by
    ```
    select * from 
    ```


## 事务
事务是平时聊得最多的数据库主题之一，但也是最容易被用错的。
> 下面的事务都指的是本地事务。
### 事务原理
TODO:

### 在Spring中应用事务
TODO：加锁操作最好放到@Transactional外面

### 事务和行锁
TODO：加行锁一定要在开启事务之后
```

```

### 事务和乐观锁

### 事务和分布式锁

### 事务和MVCC


## 索引
### 为什么要使用索引？
索引是存储引擎用于快速找到记录的一种数据结构，可以让服务器快速定位到表的指定位置。在查找数据时，存储引擎先在索引中找到对应的值，然后根据所匹配的索引记录找到对应的数据行。索引列的顺序非常重要，MySQL 只能高效的使用索引的最左前缀列。
索引具有如下优点：
1. 加快数据库的检索速度；
1. 索引降低了插入、删除、修改等维护人物的速度；
1. 减少服务器需要扫描的数据量，唯一索引可以确保每一行的唯一性；
1. 通过使用索引，可以在查询的过程中使用优化隐藏器，提高系统的性能，帮服务器避免排序和临时表；
1. 将随机 IO 变为顺序 IO。

索引具有如下缺点：
1. 需要额外的维护成本，降低数据更新的速度；
1. 占用内存和磁盘的空间。

### 按创建时机分类创建索引
1. 创建表的时候
    ```
    create table student (
        id bigint not null unique auto_increment,
        name varchar(255) not null,
        stu_num char(8) not null,
        index(stu_num)
    );
    ```
    使用explain语句查看索引是否正在使用。
    ```
    mysql> explain select * from student where stu_num = '20144749'; +----+-------------+---------+------------+------+---------------+---------+---------+-------+------+----------+-------+
    | id | select_type | table | partitions | type | possible_keys | key | key_len | ref | rows | filtered | Extra |
    +----+-------------+---------+------------+------+---------------+---------+---------+-------+------+----------+-------+
    | 1 | SIMPLE | student | NULL | ref | stu_num | stu_num | 8 | const | 1 | 100.00 | NULL |
    +----+-------------+---------+------------+------+---------------+---------+---------+-------+------+----------+-------+
    1 row in set, 1 warning (0.00 sec)
    ```
select_type=SIMPLE：表示简单select，不含union或子查询；
table=student：读取的数据表名，按读取先后排列；
type=ref：表示本表与其他表之间的关联关系；
possible_keys=stu_num：表示MySQL在搜索记录时可选用的各索引；
key=stu_num：表示MySQL实际选用的索引；
key_len=8：给出索引按字节计算的长度，key_len数值越小表示越快；
ref=const：给出关联关系中另一个数据表里的数据列的名字；
rows=1：预计读出数据行个数；
extra=NULL：与关联操作有关的信息。
1. 在已存在的表上创建（alter table）
    ```
    -- 指定前缀长度可以加快索引速度
    alter table student add unique index uniqIdx(id(10));
    -- 在MySQL中create index被映射到一个alter table语句上，它们是等价的
    create unique index uniqIdx(id(10)) on student;
    ```
    
### 按字段数量分类创建索引
1. 单列索引
上边给出的例子都属于单列索引。
1. 组合索引
    ```
    create table student (
        id bigint not null unique auto_increment,
        name varchar(255) not null,
        stu_num char(8) not null,
        index multiIdx(id, stu_num)
    );
    ```
需要注意的是组合索引遵从“最左前缀”原则：使用索引中最左边的列集来匹配行，索引中按id/name/age的顺序存放，索引可以搜索下面字段组合：(id, stu_num), id，单纯搜索stu_num不能使用索引。
同样可以使用explain分析索引的使用情况，如果possible_keys中显示multiIdx说明就是使用的上边的索引。

### 按索引功能分类创建索引
下面对普通索引（没有加UNIQUE等限制）、唯一索引（UNIQUE）、全文索引（FULLTEXT）、空间索引（SPATIAL）分别说明。
1. 普通索引
已在前面给出。
1. 唯一索引
索引列的值必须唯一，但允许有空值，如果是组合索引，则列值的组合必须唯一。
    ```
    create table student (
        id bigint not null unique auto_increment,
        name varchar(255) not null,
        stu_num char(8) not null,
        unique index uniqIdx(stu_num)
    );
    ```
1. 全文索引
只有MyISAM存储引擎支持FULLTEXT索引，并且只支持CHAR、VARCHAR、TEXT类型的列。索引总是对整列进行，不支持局部（前缀）索引。
    ```
    create table student (
        id bigint not null unique auto_increment,
        name varchar(255) not null,
        stu_num char(8) not null,
        fulltext index fullTxtIdx(name)
    );
    ```
1. 空间索引
空间索引必须在MyISAM类型的表中创建，且字段必须非空。
    ```
    create table pos (
        g geometry not null,
        spatial index spatIdx(g)
    ) engine=MyISAM;
    ```
    
### 删除索引
```
alter table student drop index uniqIdx;
-- drop index语句在内部被映射到一个alter table语句中
drop index uniqIdx on student;
```
注意：
* 添加了auto_increment约束字段的唯一索引是不能被删除的。
* 删除的列时，若目标列为索引的组成部分，则该列也会从索引中删除，如果组成索引的所有列都被删除，则整个索引被删除。


## 数据模型设计
### 概念
* 关系数据库：一个长期存储在计算机内的、有组织的、有共享的、统一管理的数据集合。它是一个按数据结构来存储和管理数据的计算机软件系统。
* SQL
* 数据库、数据库管理系统（DataBase Management System, DBMS）、数据库应用程序（DataBase Application）
* 数据库访问接口
* 表：数据库表是一系列二维数组的集合，用来存储数据和操作数据的逻辑结构。它由纵向的列和横向的行组成，行被称为记录，是组织数据的单位；列被称为字段，每一列表示记录的一个属性，都有相应的描述信息，如数据类型、数据宽度等。
* 数据类型：定义一个字段的取值范围；
* 码（主键）：能唯一标识一条记录的字段集合；
* 主码：由设计者选出的一个码，用于唯一标识一条记录；
* 主属性：属于某个码中的一个属性；
* 部分依赖
* 传递依赖

### 范式
一范式在数据库中一般是天然成立的，因为每个字段都是基本类型（有些数据库会提供自定义类型，但是用得少）。 
二范式举例来说，如果a、b合为码，若有一个属性c依赖于单个b，则说有了部分依赖，如果码只有一个属性，那必然满足二范式。 
三范式举例来说，如果a是一个码，b和c为非主属性，b依赖于a，c依赖于b，则c传递依赖于a，产生了传递依赖，就不满足三范式。 
BC范式举例来说，如果a、b是一个码，b、c是一个码，而b依赖于a，则出现了主属性的部分依赖，不满足BC范式。
总而言之：一范式不可分割，二范式无部分依赖，三范式无非主属性传递依赖，BC范式无主属性的部分和传递依赖，四范式无多值依赖


## 参考
1. 文档
[MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/)
[MySQL 5.7 Release Notes](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/)
1. [老夫整理的1000行MySQL学习笔记传授有缘人](https://blog.csdn.net/wanghao112956/article/details/96134864)
### 最佳实践
1. SQL查询经典50例
1. [你知道MySQL的Limit有性能问题吗](https://juejin.im/post/5cd2d57951882540d928c2be)
深度分页最好先用索引定位目标行，比如：`select * from tableName where id > 500000 limit 2;`
1. [为什么不用数据库存储图片？](https://www.jianshu.com/p/a4f7629e7d01)
1. [MySQL 主键自增 Auto Increment用法](https://juejin.im/post/5c99e5a8e51d45650678ac7a)
1. [你知道怎么分库分表吗？如何做到永不迁移数据和避免热点吗？](https://www.toutiao.com/i6677459303055491597)
hash取模（均匀分表）：数据迁移不方便，但无热点问题。
range（按id或时间分表）：数据迁移方便，但有热点问题。
1. [一次分表踩坑实践的探讨](https://www.cnblogs.com/crossoverJie/p/10716139.html)
1. [MySQL主从不一致情形与解决方法](https://blog.csdn.net/hardworking0323/article/details/81046408)
### 事务
1. [一次诡异的线上数据库的死锁问题排查过程](https://juejin.im/post/5cabf6dce51d456e8b07dd03)
### 索引

### JDBC
1. [【总结】编写自己的JDBC框架](https://www.cnblogs.com/jbelial/archive/2013/07/18/3199061.html)
### 数据模型设计
1. [如何解释关系数据库的第一第二第三范式？](https://www.zhihu.com/question/24696366)
《数据库系统概论》(第5版)
《大型网站系统与Java中间件实践》
http://www.cnblogs.com/zhongxinWang/p/4262650.html
http://blog.csdn.net/bluishglc/article/details/6161475
https://www.zhihu.com/question/30272728
http://www.cnblogs.com/fjdingsd/p/5273008.html
http://bbs.csdn.net/topics/120024254
### MySQL优化
1. [腾讯面试：一条SQL语句执行得很慢的原因有哪些？---不看后悔系列](https://www.cnblogs.com/kubidemanong/p/10734045.html)
偶尔很慢的原因：MySQL刷新脏页（内存->redolog->磁盘）、锁抢占（表锁、行锁，使用show processlist排查）
长期很慢的原因：未命中索引、选错索引（采样->基数大走索引基数小走全表扫描）。
索引分析：
select * from t force index(a) where c < 100 and c < 100000;
show index from t;
analyze table t;
1. [jeremycole/innodb_ruby](https://github.com/jeremycole/innodb_ruby)
1. ACID
[Mysql事务隔离级别与乐观锁的问题](https://segmentfault.com/q/1010000000585471)
[【眼见为实】自己动手实践理解数据库REPEATABLE READ && Next-Key Lock](https://www.cnblogs.com/songwenjie/p/8643684.html)
### 数据库架构
1. [不用找了，大厂在用的分库分表方案，都在这了](https://cloud.tencent.com/developer/article/1461825)

