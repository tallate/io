

这个小项目是我对数据处理的一个尝试，它包含从数据抓取、存储到挖掘的一系列功能，满足个人对感兴趣信息的获取和进一步分析。为了满足自己的需求，它大概需要满足下面几个需求：
1. 能够抓取博客网站，然后做离线分析，主要是能够对博客内容进行检索，然后将结果输出成pdf等格式，因为我更喜欢放到kindle里来批量阅读；
1. 从一个在线数据库中抓取数据，保证一次抓取的量不会太大，而且为了提高效率，用mapreduce并行抓取，然后做离线分析，包括数据的清洗（刚抓下来的数据结构不对）、分析（关联、过滤、排序等）；
> 公司里找数据组提需求罗嗦得不得了，如果是直接使用在线工具来抓取，开发数据库里的数据结构不按套路来，很多复杂的字段直接使用json来存，而且一次抓得多了就会崩了，抓得少了效率又太低，非常不方便。

<!-- more -->

## 数据采集
埋点 后端接口 分析http 数据清洗 展示与分析


## 数据处理
在线 OR 离线

## 数据挖掘
Caffe
DeepLearning4j
TensorFlow


## 参考
### 案例
[大数据采集、清洗、处理：使用MapReduce进行离线数据分析完整案例](https://blog.csdn.net/qq_35468937/article/details/81385357)
### 数据采集
1. [GitHub 上有哪些优秀的 Java 爬虫项目？](https://www.zhihu.com/question/31427895)
1. WebCollector
[CrawlScript/WebCollector](https://github.com/CrawlScript/WebCollector)
[CrawlScript/WebCollector - Examples](https://github.com/CrawlScript/WebCollector/tree/master/src/main/java/cn/edu/hfut/dmic/webcollector/example)
[WebCollector 的爬虫使用笔记](https://www.jianshu.com/p/3ffbbc45bc5c)
[Bloom Filter Calculator](https://hur.st/bloomfilter/?n=4000&p=1.0E-7&m=&k=8)
1. datasets
[PKUJohnson/OpenData](https://github.com/PKUJohnson/OpenData)
[awesomedata/awesome-public-datasets](https://github.com/awesomedata/awesome-public-datasets)
### 数据处理

### 搜索
1. [使用Elasticsearch实现推荐系统](https://www.jianshu.com/p/96c14cb3e210)
### 存储
1. [spring-hadoop - Sample Projects](https://github.com/spring-projects/spring-hadoop/wiki/Sample-Projects)
1. [spring-projects/spring-data-book](https://github.com/spring-projects/spring-data-book)
### 数据清洗

### 数据挖掘
1. [数据挖掘(data mining)，机器学习(machine learning)，和人工智能(AI)的区别是什么？ 数据科学(data science)和商业分析(business analytics)之间有什么关系？](https://www.cnblogs.com/DonJiang/p/5744535.html)
1. [FavioVazquez/ds-cheatsheets](https://github.com/FavioVazquez/ds-cheatsheets)
数据科学相关知识速查表。
1. 机器学习
[[DSC 2016] 系列活動：李宏毅 / 一天搞懂深度學習](https://www.slideshare.net/tw_dsconf/ss-62245351?qid=108adce3-2c3d-4758-a830-95d0a57e46bc&v=&b=&from_search=3)
[Deep Learning](http://www.deeplearningbook.org/)
[Deep Learning 中文翻译](https://github.com/exacity/deeplearningbook-chinese)
[Foundations of Machine Learning](https://mitpress.ublish.com/ereader/7093/?preview=#page/iii)
[Machine Learning Yearning 中文版](https://github.com/deeplearning-ai/machine-learning-yearning-cn)
[AI算法工程师手册](http://www.huaxiaozhuan.com/)
1. [ND4J: Scientific Computing on the JVM](https://github.com/deeplearning4j/nd4j)
1. [简明 Python 教程](http://www.kuqin.com/abyteofpython_cn/)
1. [TensorFlow 系列实验](https://cloud.tencent.com/developer/labs/series/10000)
1. [大数据竞赛平台——Kaggle 入门](https://blog.csdn.net/u012162613/article/details/41929171)

