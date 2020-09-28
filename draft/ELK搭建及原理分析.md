---
title: ELK 搭建及原理分析
categories: 技术点总结
tags:
  - ElasticSearch
abbrlink: 7f51b5c5
date: 2019-08-04 17:07:35
---

公司内要规范日志系统，第一步是要把原来的 ELB（没有 Logstash）改成 ELK，这里记录一下搭建过程和相关技术栈的总结。
<!-- more -->

https://www.elastic.co/cn/blog/how-to-debug-elasticsearch-source-code-in-intellij-idea
https://www.elastic.co/guide/en/kibana/current/docker.html#docker-defaults
https://www.elastic.co/guide/en/kibana/current/index.html
https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html
https://www.elastic.co/guide/en/logstash/current/docker-config.html
https://www.elastic.co/guide/en/logstash/current/pipeline.html#_inputs
https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

## 一、ELK 环境搭建
### 使用 Docker 搭建
Docker 的好处不必多说，

### 命令行搭建

### 在 OpenStack 上搭建


## 二、ELK 原理
### ElasticSearch 架构


## 三、logback和ELK
logback、ELK
encoder用logstash里的
RollingFileAppender
时区、app_name、%level、%X线程上下文{TraceId}、%msg内容、%
异步输出：AsyncAppender配一个线程池和队列，减少打日志对业务的影响
LoggerFactory构建Logger实例的时候传一个topic，作为业务标识
Kibana报表：Visualize
filebeat：配置来源索引是springlog-*，聚合输出到es
alert：一定时间段内相同message的达到一定数量会发一条报警
filter：如果是关键词keyword查得会快些


## 四、QA
### 为什么使用 FileBeat

### 为什么使用 Kafka

### 为什么不使用 Redis



## 参考
1. [Elastic Stack and Product Documentation（文档总览](https://www.elastic.co/guide/index.html)
1. [Elasticsearch Reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
1. [Kibana User Guide](https://www.elastic.co/guide/en/kibana/current/index.html)
1. [Logstash Reference](https://www.elastic.co/guide/en/logstash/current/index.html)
1. [Filebeat Reference](https://www.elastic.co/guide/en/beats/filebeat/current/index.html)

