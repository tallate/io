


## 二、GC


## 三、探针


## 四、Coroutine
### C
Protothreads - [Protothreads - Lightweight, Stackless Threads in C](http://dunkels.com/adam/pt/index.html)

### Java
kilim
quasar


## 五、Actor
初衷（在消息队列、微服务架构中都有应用） 事件流 消息链路追踪（Trace、日志、elk） 至少一次消费（幂等、redolog、重试？）
消息队列（Disruptor、Webflux、zeromq）
qmq-actor 怎么实现时间片轮转？初衷是减少线程调度损耗，因此可以采取一种权衡的实现方式，定义对某种msg的Processor，ActorScheduler调度Actor
分派任务并批量处理，处理完一条就检查一下是否超时。隔离？因为一种消息完全交给一个Actor来处理、而且有时间片限制就算一种消息发来很多也不会占用太多资源（隔离计算资源） 协程（将平均耗时长的，同一Actor内的消息借助协程实现并发处理，避免io阻塞影响） 动态限速（Qmq将总耗时短的排前面，有问题吧？） 多个消费组之间没有竞争但是同一服务多个实例之间可能存在竞争（使用协程？）
特征（事件驱动 位置透明 轻量 消息事务）




## 参考
### 协程
1. [Thread(线程)、Fiber(纤程)、coroutine(协程) 之间的区别以及...](https://blog.csdn.net/madongchunqiu/article/details/69855744)
1. [协程的历史、现在和未来](https://www.ixueshu.com/document/68735c40ec9c9a22318947a18e7f9386.html#pdfpreview)
1. [协程在天猫交易中的实践](https://wenku.baidu.com/view/92bd897fcaaedd3383c4d35d.html?from=search)
1. [在Java中使用协程（Coroutine）](http://www.blogjava.net/BlueDavy/archive/2010/01/28/311148.html)
1. [基于协程模型的分布式爬虫框架](https://www.ixueshu.com/document/e5d336e4271b8b3f318947a18e7f9386.html)
1. [基于协程的分布式RPC框架CO-RPC的设计与实现](http://www.doc88.com/p-9384812588810.html)
1. [基于协程的web服务器原型的设计与实现](http://www.doc88.com/p-2292599709635.html)
1. [基于协程的高并发的分析与研究](http://www.doc88.com/p-5955645501329.html)
### JPDA
1. [调试器工作原理](http://www.360doc.com/content/16/0921/17/7991404_592565019.shtml)
1. [简易调试器的原理](https://bbs.pediy.com/thread-206292.htm)
1. [深入 java 调试体系](https://www.ibm.com/developerworks/cn/views/java/libraryview.jsp?search_by=%E6%B7%B1%E5%85%A5+java+%E8%B0%83%E8%AF%95%E4%BD%93%E7%B3%BB)
