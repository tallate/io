---
title: 从Event Driven到Serverless
date: 2019-03-14 00:08:30
categories: 功能设计
tags: EventDriven EventBus Serverless AsyncProcessing DFA
---


* [ ] DesignPattern - 观察者模式（发布订阅模式）
* [ ] DesignPattern - Reacter
* [ ] EventDriven - 事件驱动与事件总线
* [ ] EventDriven - RxJava 中的事件驱动设计
* [ ] EventDriven - Spring Cloud Bus 的实现
* [ ] EventDriven - Guava 中EventBus的设计
* [ ] 实战 - 规则引擎
* [ ] 实战 - Serverless
* [ ] 实战 - 实时计算
* [ ] Push&Pull - 数据同步需求和推拉系统实现
* [ ] Push&Pull - 消息队列及范式
* [ ] 实战 - 监控报警系统
* [ ] AsyncProcessing - Spring MVC 中的异步处理模式DeferredResult
* [ ] AsyncProcessing - 异步IO框架epoll中的事件驱动设计
* [ ] 实战 - 设计一个异步请求客户端
* [ ] Automata - 自动机理论
* [ ] Automata - 进程 / 线程调度中的状态机模型
* [ ] Automata - 编译原理里的有限状态机模型
* [ ] Automata - ABNF
* [ ] 实战 - 订单系统的状态机设计
* [ ] 实战 - 设计一个网络协议


## 一、DesignPattern
### 观察者模式

### Reactor模式


## 二、Event Driven

libevent
[libevent源码深度剖析](https://blog.csdn.net/sparkliang/article/details/4957667)

### 规则引擎

1. [大数据：美团酒旅实时数据规则引擎应用实践](https://www.imooc.com/article/26960)

### Serverless
随着云系统的发展，基于事件驱动的Serverless架构开始有成为SOA的替代的趋势，Serverless允许开发者为定义要为某个事件调用的函数，然后函数本身可以生成更多的事件，而这些事件又由其他函数处理。Serverless没有要求开发者维护服务器的运行，并且不必担心在负载增加时运行其他服务器。Serverless是比SaaS（软件即服务）模式具有更高抽象层次的云服务模式，可以称之为**FaaS**（功能即服务），它只关注业务逻辑的实现，无需关注服务器资源，甚至是软件的架构也基本由云服务提供商所提供（或者说限制）。

1. [github - knative/docs](https://github.com/knative/docs)

## 三、Push&Pull

### QMQ

### RocketMQ

### Kafka


## 四、Async 6Processing



## 五、Automata
我问过一个为订单系统设计过状态机的同事，状态扭转这么复杂是怎么保证正确性的，他的回答是


## 参考

