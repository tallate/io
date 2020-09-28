
## 参考
1. Github https://github.com/junit-team/junit5
1. API http://junit.org/junit5/docs/current/api/overview-summary.html

## 构建启动器
### AllDefaultPossibilitiesBuilder
看runnerForClass(Class<?> testClass)
testClass为目标测试类，这个方法的主要作用是使用所有默认的构建器尝试为目标类构建一个启动器，用的比较多的是 `AnnotatedBuilder` 。
### AnnotatedBuilder
看runnerForClass()
主要目的是解析 `@RunWith` 注解，用反射方法实例化之，实际上这个注解就是为了声明想要构建的启动器。
### SpringJUnit4ClassRunner
为Spring应用准备的启动器。
createTestContextManager() 创建上下文管理器，并设置TestExecutionListener（包括ServletTestExecutionListener）。
### TestContextManager
管理TestContext和TestExecutionListener，生成测试用例对象。
prepareTestInstance() 准备测试用例对象。

## 预处理
### ServletTestExecutionListener
预处理Spring容器。
### DependencyInjectionTestExecutionListener
处理依赖，包括调用AutowiredAnnotationBeanPostProcessor的方法来初始化@Autowired的属性和方法。
## 执行
### JUnitCore
看 `run(Runner runner)`
这是一个外观类，用于执行测试类，需要在命令行启动时就是使用它来启动的。
### RunNotifier和RunListener
观察者模式，在单元测试的相应阶段会调用注册在RunNotifier中的RunListener的对应方法（指的是@Before、@After、@Test这些阶段）。

## 并发支持
1. 使用RunnerScheduler来管理Statement的执行
一个Statement可以是目标方法，在执行器父类ParentRunner中使用一个Runnable表示，并放到一个RunnerScheduler中执行，这意味着根据执行策略的不同，多个Statement可以是串行的或并行的。
1. 在测试用例中不方便使用多线程
JUnitCore和TestRunner的main方法都是在主线程执行完毕后就调用System.exit退出的。



