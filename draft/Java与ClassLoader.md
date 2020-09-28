---
title: Java 与 ClassLoader
abbrlink: 8ada3a78
date: 2019-10-19 15:27:39
categories: 技术点总结
tags: [JVM, ClassLoader]
---



### Java 类加载顺序

如果项目中的类和三方jar包中的类的全类名一致，则项目启动后加载哪个类是不确定的，但类加载器会选择第一次加载的类为准，之后的不会覆盖。
在Idea中类的加载顺序是可以编辑的，可以在工程中调整加载顺序：
```
<orderEntry type="sourceFolder" forTests="false" />
<orderEntry type="module" module-name="common" />
<orderEntry type="library" name="Maven: org.springframework.boot:spring-boot-starter-web:2.1.7.RELEASE" level="project" />
```

### 自定义ClassLoader

