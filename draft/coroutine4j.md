


## Coroutine
kilim
quasar


## Example - Actor
初衷（在消息队列、微服务架构中都有应用） 事件流 消息链路追踪（Trace、日志、elk） 至少一次消费（幂等、redolog、重试？）
消息队列（Disruptor、Webflux、zeromq）
qmq-actor 怎么实现时间片轮转？初衷是减少线程调度损耗，因此可以采取一种权衡的实现方式，定义对某种msg的Processor，ActorScheduler调度Actor
分派任务并批量处理，处理完一条就检查一下是否超时。隔离？因为一种消息完全交给一个Actor来处理、而且有时间片限制就算一种消息发来很多也不会占用太多资源（隔离计算资源） 协程（将平均耗时长的，同一Actor内的消息借助协程实现并发处理，避免io阻塞影响） 动态限速（Qmq将总耗时短的排前面，有问题吧？） 多个消费组之间没有竞争但是同一服务多个实例之间可能存在竞争（使用协程？）
特征（事件驱动 位置透明 轻量 消息事务）



## 参考
1. [Thread(线程)、Fiber(纤程)、coroutine(协程) 之间的区别以及...](https://blog.csdn.net/madongchunqiu/article/details/69855744)


