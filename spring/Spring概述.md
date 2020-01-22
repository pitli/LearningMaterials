### Spring 框架的优点 

- `非侵入式设计`：使应用程序代码对框架的依赖最小化.
- `方便解耦、简化开发`：可将所有对象的创建和依赖关系的维护工作交给Spring管理，降低组件的耦合性.
- `支持AOP`：可将一些通用任务,如安全、事务、日志等进行集中式处理，提高程序的复用性.
- `支持声明式事务处理`：配置即可完成对事务的管理，无需手动编程.
- `方便程序测试`：对Junit4支持，通过注解方便测试Spring程序.
- `方便集成各种优秀框架`：不排斥各种优秀的开源框架，提供了对各种优秀框架的直接支持.
- `降低Java EE API使用难度`：对开发中一些难用的API提供了封装(如JDBC、JavaMail等).

------

### Spring 的体系结构 

1. **Core Container(核心容器)**：Spring 的核心容器是其他模块建立的基础，具体组成模块如下:
   - `Beans模块`：提供BeanFactory，是工厂模式的经典实现,Spring将管理对象称为Bean.
   - `Core 核心模块`：提供了Spring的基本组成部分，包括IOC和DI功能.
   - `Context 上下文模块`：建立在Core和Beans模块的基础之上，是访问定义和配置的任何对象的媒介，其中ApplicationContext 接口是上下文模块的焦点  .
   - `Context-support 模块`：提供了对第三方库嵌入 Spring 应用的集成支持，比如缓存(EhCache)、邮件(JavaMail)、任务调度(Quartz)、模板引擎(FreeMarker).
   - `SpEL模块`：是 Spring 3 . 0 后新增的模块，它提供了 Spring Expression Language 支持，是运行时查询和操作对象图的强大的表达式语言.
2. **Data Access/lntegration (数据访问/集成)**：数据访问/集成层包括 JDBC、ORM、OXM、JMS和Transactions模块，具体介绍如下：
   - `JDBC模块`：提供了JDBC的抽象层，减少了开发过程中对数据库操作的编码.
   - `ORM模块`：对流行的对象关系映射API，包括JPA和Hibernate提供了集成与支持.
   - `OXM模块`：提供了支持对象/XML映射的抽象层实现，如JAXB、Castor、XMLBeans、JiBX和XStream.
   - `JMS模块`：Java消息传递服务,包含使用和产生信息的特性，自4.1版本后支持与Spring-message模块集成.
   - `Transactions事务模块`：支持对实现特殊接口以及所有POJO了的编程和声明式的事务管理.
3. **WEB**：Spring 的 Web 层包括 WebSocket 、 Servlet 、 Web 和 Portlet 模块，具体介绍如下：
   - `WebSocket模块`：Spring4.0以后新增的模块，提供了WebSocket和SockJS的实现，以及对STOMP的支持.
   - `Servlet模块`：也称为Spring-webmvc模块，包含了Spring的模型—视图—控制器(MVC)和REST Web Services实现的Web应用程序.
   - `Web模块`：提供基本的Web开发集成特性，例如：多文件上传、使用Servlet监听器来初始化IOC容器以及Wen应用上下文.
   - `Portlet模块`：提供了在Portlet环境中使用MVC实现，类似Servlet模块的功能.
4. **其他模块**：Spring的其他模块还有 AOP 、 Aspects 、 Instrumentation 以及 Test 模块，具体介绍如下：
   - `AOP模块`：面向切面编程，允许定义方法拦截器和切入点，将代码按照功能分离，以降低耦合性.
   - `Aspects模块`：与AspectJ集成，AspectJ是功能强大且成熟的面向切面编程(AOP)框架.
   - `Instrumentation模块`：提供类工具的支持和类加载器的实现，可在特定应用服务器中使用.
   - `Messaging模块`：Spring4.0以后新增，提供对消息传递体系结构和协议的支持.
   - `Test模块`：提供对单元测试和集成测试的支持.

------

### Spring的基础包

[Jar包下载地址](https://repo.spring.io/libs-release/org/springframework/spring/4.2.6.RELEASE/)

- **spring-core-4.3.6.RELEASE.jar**：包含Spring框架基本的核心工具类，其他组件都要用到这个包的类，是其他组件的基本核心.
- **spring-beans-4.3.6.RELEASE.jar**：所有应用都要用到的Jar包，包含访问配置文件、创建和管理Bean以及进行IOC或DI操作相关的类.
- **spring-context-4.3.6.RELEASE.jar**：提供了在基础IOC功能上的扩展服务，还提供了企业级服务的支持，如邮件服务、任务调度、JNDI定位、EJB集成、远程访问、缓存以及各种视图层框架的封装等.
- **spring-expression-4.3.6.RELEASE.jar**：定义Spring的表达式语言.

------

