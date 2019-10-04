## Linux IO模型
![X](http://47.88.24.11/imgs/Linux内核-IO/Linux整体结构.png "Linux整体结构")
应用程序调用内核IO函数的过程如下图所示：
![X](http://47.88.24.11/imgs/Linux内核-IO/IO系统调用过程.png "IO系统调用过程")
处于OS的安全性等的考虑，进程无法直接操作I/O设备，必须通过系统调用来请求内核完成I/O动作，而内核会为每个I/O设备维护一个Buffer。
1. 用户进程发起请求；
1. 内核接收到请求后，从I/O设备中获取数据到Buffer中；
1. 将Buffer中的数据拷贝到用户进程的地址空间，该用户进程获取到数据后响应给客户端。

在整个请求过程中，数据输入至Buffer需要时间，从Buffer复制数据到进程也需要时间，这个等待时间是限制I/O效率的罪魁祸首，根据等待方式的不同，I/O动作可以分为以下五种模式：
* 阻塞I/O（Blocking I/O）
* 非阻塞I/O（Non-Blocking I/O）
* I/O复用（I/O Multiplexing）
* 信号驱动的I/O（Signal Driven I/O）
* 异步I/O（Asynchronous I/O）


### 零拷贝



## 参考
1. [NIO 相关基础篇三 - 五种I/O模型、零拷贝](https://v2ex.com/t/571465)
1. 《UNP》