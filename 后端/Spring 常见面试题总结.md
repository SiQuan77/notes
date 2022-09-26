> 参考[Spring 常见面试题总结 | JavaGuide](https://javaguide.cn/system-design/framework/spring/spring-knowledge-and-questions-summary.html#spring-基础)，感谢Guide哥！

# Spring 常见面试题总结

​	这篇文章主要是想通过一些问题，加深大家对于 Spring 的理解，所以不会涉及太多的代码！

​	下面的很多问题我自己在使用 Spring 的过程中也并没有注意，自己也是临时查阅了很多资料和书籍补上的。网上也有一些很多关于 Spring 常见问题/面试题整理的文章，我感觉大部分都是互相 copy，而且很多问题也不是很好，有些回答也存在问题。所以，自己花了一周的业余时间整理了一下，希望对大家有帮助。

## Spring 基础

### 什么是 Spring 框架?

​	Spring 是一款开源的轻量级 Java 开发框架，旨在提高开发人员的开发效率以及系统的可维护性。

​	我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发，比如说 Spring 支持 IoC（Inverse of Control:**控制反转**） 和 AOP(Aspect-Oriented Programming:**面向切面编程**)、可以很方便地对数据库进行访问、可以很方便地集成第三方组件（电子邮件，任务，调度，缓存等等）、对单元测试支持比较好、支持 RESTful Java 应用程序的开发。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152125160.png)

​	Spring 最核心的思想就是不重新造轮子，开箱即用，提高开发效率。Spring 翻译过来就是春天的意思，可见其目标和使命就是为 Java 程序员带来春天啊！感动！

​	🤐 多提一嘴 ： **语言的流行通常需要一个杀手级的应用，Spring 就是 Java 生态的一个杀手级的应用框架。**

​	Spring 提供的核心功能主要是 **IoC** 和 **AOP**。学习 Spring ，一定要把 IoC 和 AOP 的核心思想搞懂！

### Spring 包含的模块有哪些？

**Spring4.x 版本** ：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152152857.png)

**Spring5.x 版本** ：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152153385.png)

​	Spring5.x 版本中 Web 模块的 <u>Portlet 组件已经被废弃</u>掉，同时增加了用于异步响应式处理的 WebFlux 组件。

Spring 各个模块的依赖关系如下：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152153575.png)

#### Core Container

​	Spring 框架的**核心模块**，也可以说是**基础模块**，主要提供 **IoC 依赖注入功能的支持**。Spring 其他所有的功能基本都需要依赖于该模块，我们从上面那张 Spring 各个模块的依赖关系图就可以看出来。

- **spring-core** ：Spring 框架基本的核心工具类。
- **spring-beans** ：提供对 bean 的创建、配置和管理等功能的支持。
- **spring-context** ：提供对国际化、事件传播、资源加载等功能的支持。
- **spring-expression** ：提供对表达式语言（Spring Expression Language） SpEL 的支持，只依赖于 core 模块，不依赖于其他模块，可以单独使用。

#### AOP

- **spring-aspects** ：该模块为与 AspectJ 的集成提供支持。
- **spring-aop** ：提供了面向切面的编程实现。
- **spring-instrument** ：提供了为 JVM 添加代理（agent）的功能。 具体来讲，它为 Tomcat 提供了一个织入代理，能够为 Tomcat 传递类文件，就像这些文件是被类加载器加载的一样。没有理解也没关系，这个模块的使用场景非常有限。

#### Data Access/Integration

- **spring-jdbc** ：提供了对数据库访问的抽象 JDBC。不同的数据库都有自己独立的 API 用于操作数据库，而 Java 程序只需要和 JDBC API 交互，这样就屏蔽了数据库的影响。
- **spring-tx** ：提供对事务的支持。
- **spring-orm** ： 提供对 Hibernate、JPA 、iBatis 等 ORM 框架的支持。
- **spring-oxm** ：提供一个抽象层支撑 OXM(Object-to-XML-Mapping)，例如：JAXB、Castor、XMLBeans、JiBX 和 XStream 等。
- **spring-jms** : 消息服务。自 Spring Framework 4.1 以后，它还提供了对 spring-messaging 模块的继承。

#### Spring Web

- **spring-web** ：对 Web 功能的实现提供一些最基础的支持。
- **spring-webmvc** ： 提供对 Spring MVC 的实现。
- **spring-websocket** ： 提供了对 WebSocket 的支持，WebSocket 可以让客户端和服务端进行双向通信。
- **spring-webflux** ：提供对 WebFlux 的支持。WebFlux 是 Spring Framework 5.0 中引入的新的响应式框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步。

#### Messaging

​	**spring-messaging** 是从 Spring4.0 开始新加入的一个模块，主要职责是为 Spring 框架集成一些<u>基础的报文传送应用</u>。

####  Spring Test

​	Spring 团队提倡测试驱动开发（TDD）。有了控制反转 (IoC)的帮助，单元测试和集成测试变得更简单。

​	Spring 的测试模块对 JUnit（单元测试框架）、TestNG（类似 JUnit）、Mockito（主要用来 Mock 对象）、PowerMock（解决 Mockito 的问题比如无法模拟 final, static， private 方法）等等常用的测试框架支持的都比较好。

### Spring,Spring MVC,Spring Boot 之间什么关系?

​	很多人对 Spring,Spring MVC,Spring Boot 这三者傻傻分不清楚！这里简单介绍一下这三者，其实很简单，没有什么高深的东西。

​	Spring 包含了**多个功能模块**（上面刚刚提高过），其中最重要的是 Spring-Core（主要提供 IoC 依赖注入功能的支持） 模块， Spring 中的其他模块（比如 Spring MVC）的功能实现基本都需要依赖于该模块。

​	下图对应的是 Spring4.x 版本。目前最新的 5.x 版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152152857.png)

​	Spring MVC 是 Spring 中的一个**很重要的模块**，主要赋予 Spring **快速构建 MVC 架构的 Web 程序的能力**。MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将**业务逻辑**、**数据**、**显示**分离来组织代码。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152157914.png)

​	使用 Spring 进行开发各种配置过于麻烦比如开启某些 Spring 特性时，需要用 XML 或 Java 进行显式配置。于是，Spring Boot 诞生了！

​	Spring 旨在简化 J2EE 企业应用程序开发。Spring Boot 旨在**简化 Spring 开发**（减少配置文件，开箱即用！）。Spring Boot 只是简化了配置，如果你需要构建 MVC 架构的 Web 程序，你还是需要使用 Spring MVC 作为 MVC 框架，只是说 **Spring Boot 帮你简化了 Spring MVC 的很多配置，真正做到开箱即用**！

## Spring IoC

### 谈谈自己对于 Spring IoC 的了解

​	**IoC（Inverse of Control:控制反转）** 是一种<u>设计思想</u>，而不是一个具体的技术实现。IoC 的思想就是**将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理**。不过， IoC 并非 Spring 特有，在其他语言中也有应用。

**为什么叫控制反转？**

- **控制** ：指的是对象创建（实例化、管理）的权力
- **反转** ：控制权交给外部环境（Spring 框架、IoC 容器）

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152159190.png)

​	将对象之间的相互依赖关系交给 IoC 容器来管理，并**由 IoC 容器完成对象的注入**。这样可以很大程度上<u>简化应用的开发</u>，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，**完全不用考虑对象是如何被创建出来的**。

​	在实际项目中一个 Service 类可能依赖了很多其他的类，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。在 Spring 中， IoC 容器是 Spring 用来实现 IoC 的载体， **IoC 容器实际上就是个 Map（key，value）**，<u>Map 中存放的是各种对象</u>。

​	Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。

相关阅读：

- [IoC 源码阅读](https://javadoop.com/post/spring-ioc)
- [面试被问了几百遍的 IoC 和 AOP ，还在傻傻搞不清楚？](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486938&idx=1&sn=c99ef0233f39a5ffc1b98c81e02dfcd4&chksm=cea24211f9d5cb07fa901183ba4d96187820713a72387788408040822ffb2ed575d28e953ce7&token=1736772241&lang=zh_CN#rd)

------

> 另一种解释：参考[Spring IoC有什么好处呢？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/23277575/answer/169698662)，感谢Mingqi！



​	要了解控制反转( Inversion of Control ), 我觉得有必要先了解软件设计的一个重要思想：依赖倒置原则（Dependency Inversion Principle ）。

​	**什么是依赖倒置原则？**假设我们设计一辆汽车：先设计轮子，然后根据轮子大小设计底盘，接着根据底盘设计车身，最后根据车身设计好整个汽车。这里就出现了一个“依赖”关系：汽车依赖车身，车身依赖底盘，底盘依赖轮子。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161025962.png)

​	这样的设计看起来没问题，但是**可维护性却很低**。假设设计完工之后，上司却突然说根据市场需求的变动，要我们把车子的轮子设计都改大一码。这下我们就蛋疼了：因为我们是根据轮子的尺寸设计的底盘，轮子的尺寸一改，底盘的设计就得修改；同样因为我们是根据底盘设计的车身，那么车身也得改，同理汽车设计也得改——整个设计几乎都得改！

​	我们现在换一种思路。我们<u>先设计汽车的大概样子</u>，然后根据汽车的样子来设计车身，根据车身来设计底盘，最后根据底盘来设计轮子。这时候，依赖关系就倒置过来了：**轮子依赖底盘， 底盘依赖车身， 车身依赖汽车**。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161026157.png)

​	这时候，上司再说要改动轮子的设计，我们就只需要改动轮子的设计，而不需要动底盘，车身，汽车的设计了。这就是依赖倒置原则——把原本的高层建筑依赖底层建筑“倒置”过来，变成**底层建筑依赖高层建筑**。<u>高层建筑决定需要什么，底层去实现这样的需求</u>，但是高层并不用管底层是怎么实现的。这样就不会出现前面的“牵一发动全身”的情况。



​	控制反转（Inversion of Control） 就是依赖倒置原则的一种代码设计的思路。具体采用的方法就是所谓的依赖注入（Dependency Injection）。其实这些概念初次接触都会感到云里雾里的。说穿了，这几种概念的关系大概如下：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161027883.jpeg)

​	为了理解这几个概念，我们还是用上面汽车的例子。只不过这次换成代码。我们先定义四个Class，车，车身，底盘，轮胎。然后初始化这辆车，最后跑这辆车。代码结构如下：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161027764.jpeg)

​	这样，就相当于上面第一个例子，上层建筑依赖下层建筑——每一个类的构造函数都直接调用了底层代码的构造函数。下层建筑以**依赖和聚合**的形式被上层建筑使用（即上层建筑有下层建筑的对象但在声明的时候并不直接new出来）。假设我们需要改动一下轮胎（Tire）类，**把它的尺寸变成动态**的，而不是一直都是30。我们需要这样改：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161028603.png)

​	由于我们修改了轮胎的定义，为了让整个程序正常运行，我们需要做以下改动：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161028639.jpeg)

​	由此我们可以看到，**仅仅是为了修改轮胎的构造函数，这种设计却需要修改整个上层所有类的构造函数**！在软件工程中，这样的设计几乎是不可维护的——在实际工程项目中，有的类可能会是几千个类的底层，如果每次修改这个类，我们都要修改所有以它作为依赖的类，那软件的维护成本就太高了。

​	所以我们需要进行控制反转（IoC），及上层控制下层，而不是下层控制着上层。我们用依赖注入（Dependency Injection）这种方式来实现控制反转。**所谓依赖注入，就是把<u>底层类作为参数</u>传入上层类，实现上层类对下层类的“控制**”。这里我们用**构造方法传递的依赖注入方式**重新写车类的定义：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161034975.jpeg)

​	这里我们再把轮胎尺寸变成动态的，同样为了让整个系统顺利运行，我们需要做如下修改：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161034531.jpeg)



​	看到没？这里我只需要修改轮胎类就行了，不用修改其他任何上层类。这显然是**更容易维护的代码**。不仅如此，在实际的工程中，这种设计模式还有利于<u>不同组的协同合作和单元测试</u>：比如开发这四个类的分别是四个不同的组，那么只要定义好了接口，四个不同的组可以同时进行开发而不相互受限制；而对于单元测试，如果我们要写Car类的单元测试，就只需要Mock一下Framework类传入Car就行了，而不用把Framework, Bottom, Tire全部new一遍再来构造Car。

​	这里我们是采用的构造函数传入的方式进行的依赖注入。其实还有另外两种方法：<u>Setter传递</u>和<u>接口传递</u>。这里就不多讲了，核心思路都是一样的，都是为了实现控制反转。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161036058.jpeg)

​	那什么是**控制反转容器(IoC Container)**呢？其实上面的例子中，对车类进行初始化的那段代码发生的地方，就是控制反转容器。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161036221.jpeg)

​	显然你也应该观察到了，因为采用了依赖注入，在初始化的过程中就不可避免的会写大量的new。这里IoC容器就解决了这个问题。**这个容器可以<u>自动</u>对你的代码进行初始化，你只需要维护一个Configuration（可以是xml可以是一段代码），而不用每次初始化一辆车都要亲手去写那一大段初始化的代码**。这是引入IoC Container的第一个好处。

​	IoC Container的第二个好处是：**我们在创建实例的时候不需要了解其中的细节。**在上面的例子中，我们自己手动创建一个车instance时候，是从底层往上层new的：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161037618.jpeg)



​	这个过程中，我们需要了解整个Car/Framework/Bottom/Tire类构造函数是怎么定义的，才能一步一步new/注入。而IoC Container在进行这个工作的时候是反过来的，它先从最上层开始往下**找依赖关系**，到达<u>最底层之后再往上一步一步new</u>（有点像深度优先遍历）：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161038309.jpeg)

​	这里IoC Container可以**直接隐藏具体的创建实例的细节**，在我们来看它就像一个工厂：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209161038512.jpeg)

​	我们就像是工厂的客户。我们只需要向工厂请求一个Car实例，然后它就给我们按照Config创建了一个Car实例。我们完全不用管这个Car实例是怎么一步一步被创建出来。

​	实际项目中，有的Service Class可能是十年前写的，有几百个类作为它的底层。假设我们新写的一个API需要实例化这个Service，我们总不可能回头去搞清楚这几百个类的构造函数吧？IoC Container的这个特性就很完美的解决了这类问题——**因为这个架构要求你在写class的时候需要写相应的Config文件，所以你要初始化很久以前的Service类的时候，前人都已经写好了Config文件，你直接在需要用的地方注入这个Service就可以了**。这大大增加了项目的可维护性且降低了开发难度。





### 什么是 Spring Bean？

​	简单来说，Bean 代指的就是**那些被 IoC 容器所管理的对象**。我们需要告诉 IoC 容器帮助我们管理哪些对象，这个是通过<u>配置元数据</u>来定义的。配置元数据可以是 **XML 文件**、**注解**或者 **Java 配置类**。

```xml
<!-- Constructor-arg with 'value' attribute -->
<bean id="..." class="...">
   <constructor-arg value="..."/>
</bean>
```

​	下图简单地展示了 IoC 容器如何使用配置元数据来管理对象。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152202859.png)

​	`org.springframework.beans`和 `org.springframework.context` 这两个包是 IoC 实现的基础，如果想要研究 IoC 相关的源码的话，可以去看看

### 将一个类声明为 Bean 的注解有哪些?

- `@Component` ：<u>通用的注解</u>，可标注任意类为 `Spring` 组件。如果一个 Bean 不知道属于哪个层，可以使用`@Component` 注解标注。
- `@Repository` : 对应持久层即 Dao 层，主要用于数据库相关操作。
- `@Service` : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
- `@Controller` : 对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。

### @Component 和 @Bean 的区别是什么？

- `@Component` 注解作用于**类**，而`@Bean`注解作用于**方法**。
- `@Component`通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是<u>我们在标有该注解的方法中定义产生这个 bean</u>,`@Bean`告诉了 Spring 这是**某个类的实例**，当我需要用它的时候还给我。
- `@Bean` 注解比 `@Component` 注解的**自定义性更强**，而且很多地方我们只能通过 `@Bean` 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。

`@Bean`注解使用示例：

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```

​	上面的代码相当于下面的 xml 配置

```xml
<beans>
    <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```

​	下面这个例子是通过 `@Component` 无法实现的。

```java
@Bean
public OneService getService(status) {
    case (status)  {
        when 1:
                return new serviceImpl1();
        when 2:
                return new serviceImpl2();
        when 3:
                return new serviceImpl3();
    }
}
```

### 注入 Bean 的注解有哪些？

​	Spring 内置的 `@Autowired` 以及 JDK 内置的 `@Resource` 和 `@Inject` 都可以用于注入 Bean。

| Annotaion    | Package                            | Source       |
| ------------ | ---------------------------------- | ------------ |
| `@Autowired` | `org.springframework.bean.factory` | Spring 2.5+  |
| `@Resource`  | `javax.annotation`                 | Java JSR-250 |
| `@Inject`    | `javax.inject`                     | Java JSR-330 |

​	`@Autowired` 和`@Resource`使用的比较多一些。

### @Autowired 和 @Resource 的区别是什么？

​	`Autowired` 属于 Spring **内置的注解**，默认的注入方式为`byType`（**根据类型进行匹配**），也就是说会优先根据<u>接口类型</u>去匹配并注入 Bean （接口的实现类）。**这会有什么问题呢？** 当一个接口存在**多个实现类**的话，`byType`这种方式就无法正确注入对象了，因为这个时候 Spring 会同时找到多个满足条件的选择，默认情况下它自己不知道选择哪一个。

​	这种情况下，注入方式会变为 `byName`（**根据名称进行匹配**），这个名称通常就是类名（首字母小写）。就比如说下面代码中的 `smsService` 就是我这里所说的名称，这样应该比较好理解了吧。

```java
// smsService 就是我们上面所说的名称
@Autowired
private SmsService smsService;
```

​	举个例子，`SmsService` 接口有两个实现类: `SmsServiceImpl1`和 `SmsServiceImpl2`，且它们都已经被 Spring 容器所管理。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Autowired
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Autowired
private SmsService smsServiceImpl1;
// 正确注入  SmsServiceImpl1 对象对应的 bean
// smsServiceImpl1 就是我们上面所说的名称
@Autowired
@Qualifier(value = "smsServiceImpl1")
private SmsService smsService;
```

​	我们还是建议**通过 `@Qualifier` 注解来显示指定名称**而不是依赖变量的名称。`@Resource`属于 JDK 提供的注解，默认注入方式为 `byName`。如果无法通过名称匹配到对应的 Bean 的话，注入方式会变为`byType`。

​	`@Resource` 有两个比较重要且日常开发常用的属性：`name`（名称）、`type`（类型）。

```java
public @interface Resource {
    String name() default "";
    Class<?> type() default Object.class;
}
```

​	如果仅指定 `name` 属性则注入方式为`byName`，如果仅指定`type`属性则注入方式为`byType`，如果同时指定`name` 和`type`属性（不建议这么做）则注入方式为`byType`+`byName`。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Resource
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Resource
private SmsService smsServiceImpl1;
// 正确注入 SmsServiceImpl1 对象对应的 bean（比较推荐这种方式）
@Resource(name = "smsServiceImpl1")
private SmsService smsService;
```

简单总结一下：

- `@Autowired` 是 Spring 提供的注解，`@Resource` 是 JDK 提供的注解。
- `Autowired` 默认的注入方式为`byType`（根据类型进行匹配），`@Resource`默认注入方式为 `byName`（根据名称进行匹配）。
- 当一个接口存在多个实现类的情况下，`@Autowired` 和`@Resource`都需要<u>通过名称</u>才能正确匹配到对应的 Bean。`Autowired` 可以通过 `@Qualifier` 注解来显示指定名称，`@Resource`可以通过 `name` 属性来显示指定名称。

### Bean 的作用域有哪些?

Spring 中 Bean 的作用域通常有下面几种：

- **singleton** : IoC 容器中**只有唯一的 bean 实例**。Spring 中的 bean 默认都是**单例的**，是对单例设计模式的应用。
- **prototype** : 每次获取都会**创建一个新的 bean 实例**。也就是说，连续 `getBean()` 两次，得到的是不同的 Bean 实例。
- **request** （仅 Web 应用可用）: 每一次 HTTP 请求都会**产生一个新的 bean**（请求 bean），<u>该 bean 仅在当前 HTTP request 内有效</u>。
- **session** （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会**产生一个新的 bean**（会话 bean），<u>该 bean 仅在当前 HTTP session 内有效</u>。
- **application/global-session** （仅 Web 应用可用）： 每个 Web 应用在**启动时创建一个 Bean**（应用 Bean），该 bean 仅在当前应用启动时间内有效。
- **websocket** （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。

**如何配置 bean 的作用域呢？**

xml 方式：

```xml
<bean id="..." class="..." scope="singleton"></bean>
```

注解方式：

```java
@Bean
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public Person personPrototype() {
    return new Person();
}
```

### 单例 Bean 的线程安全问题了解吗？

​	大部分时候我们并没有在项目中使用多线程，所以很少有人会关注这个问题。**单例 Bean 存在线程问题**，主要是因为当多个线程操作同一个对象的时候是存在<u>资源竞争</u>的。

常见的有两种解决办法：

1. 在 Bean 中尽量**避免定义可变的成员变量**。
2. 在类中定义一个 `ThreadLocal` 成员变量，将需要的可变成员变量保存在 `ThreadLocal` 中（推荐的一种方式）。

​	不过，大部分 Bean 实际都是**无状态**（没有实例变量）的（比如 Dao、Service），这种情况下， Bean 是线程安全的。

### Bean 的生命周期了解么?

> 下面的内容整理自：[https://yemengying.com/2016/07/14/spring-bean-life-cycle/open in new window](https://yemengying.com/2016/07/14/spring-bean-life-cycle/) ，除了这篇文章，再推荐一篇很不错的文章 ：[[Spring Bean的生命周期（非常详细） - Chandler Qian - 博客园 (cnblogs.com)])](https://www.cnblogs.com/zrtqsk/p/3735273.html)

- Bean 容器找到配置文件中 Spring Bean 的定义。
- Bean 容器利用 Java Reflection API（反射） 创建一个 Bean 的实例。
- 如果涉及到一些属性值 利用 `set()`方法设置一些属性值。
- 如果 Bean 实现了 `BeanNameAware` 接口，调用 `setBeanName()`方法，传入 Bean 的名字。
- 如果 Bean 实现了 `BeanClassLoaderAware` 接口，调用 `setBeanClassLoader()`方法，传入 `ClassLoader`对象的实例。
- 如果 Bean 实现了 `BeanFactoryAware` 接口，调用 `setBeanFactory()`方法，传入 `BeanFactory`对象的实例。
- 与上面的类似，如果实现了其他 `*.Aware`接口，就调用相应的方法。
- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessBeforeInitialization()` 方法
- 如果 Bean 实现了`InitializingBean`接口，执行`afterPropertiesSet()`方法。
- 如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。
- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessAfterInitialization()` 方法
- 当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。
- 当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152211889.png)

## Spring AoP

### 谈谈自己对于 AOP 的了解

​	AOP(Aspect-Oriented Programming:面向切面编程)能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）**封装起来**，便于<u>减少系统的重复代码</u>，<u>降低模块间的耦合度</u>，并有利于未来的<u>可拓展性</u>和<u>可维护性</u>。

​	Spring AOP 就是基于**动态代理**的，如果要代理的对象，实现了某个接口，那么 Spring AOP 会使用 **JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候 Spring AOP 会使用 **Cglib** 生成一个被代理对象的子类来作为代理，如下图所示：

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152214344.png)

​	当然你也可以使用 **AspectJ** ！Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AOP 切面编程设计到的一些专业术语：

| 术语              |                             含义                             |
| :---------------- | :----------------------------------------------------------: |
| 目标(Target)      |                       被通知的**对象**                       |
| 代理(Proxy)       |           向目标对象应用通知之后创建的**代理对象**           |
| 连接点(JoinPoint) |       目标对象的所属类中，定义的**所有方法**均为连接点       |
| 切入点(Pointcut)  | 被切面拦截 / **增强**的连接点（切入点一定是连接点，连接点不一定是切入点，被增强的方法） |
| 通知(Advice)      | 增强的逻辑 / 代码，也即**拦截到目标对象的连接点之后要做的事情** |
| 切面(Aspect)      |                切入点(Pointcut)+通知(Advice)                 |
| Weaving(织入)     |       将通知应用到目标对象，进而生成代理对象的过程动作       |

### Spring AOP 和 AspectJ AOP 有什么区别？

​	**Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。** Spring AOP 基于代理(Proxying)，而 AspectJ 基于**字节码操作**(Bytecode Manipulation)。

​	Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比 Spring AOP 快很多。

### AspectJ 定义的通知类型有哪些？

- **Before**（前置通知）：目标对象的方法调用之前触发
- **After** （后置通知）：目标对象的方法调用之后触发
- **AfterReturning**（返回通知）：目标对象的方法调用完成，在返回结果值之后触发
- **AfterThrowing**（异常通知） ：目标对象的方法运行中抛出 / 触发异常后触发。AfterReturning 和 AfterThrowing 两者互斥。如果方法调用成功无异常，则会有返回值；如果方法抛出了异常，则不会有返回值。
- **Around**： （环绕通知）编程式控制目标对象的方法调用。环绕通知是所有通知类型中**可操作范围最大的一种**，因为它可以直接拿到目标对象，以及要执行的方法，所以环绕通知可以**任意的在目标对象的方法调用前后搞事**，甚至不调用目标对象的方法。

### 多个切面的执行顺序如何控制？

1、通常使用`@Order` 注解直接定义切面顺序

```java
// 值越小优先级越高
@Order(3)
@Component
@Aspect
public class LoggingAspect implements Ordered {
```

**2、实现`Ordered` 接口重写 `getOrder` 方法。**

```java
@Component
@Aspect
public class LoggingAspect implements Ordered {
    // ....
    @Override
    public int getOrder() {
        // 返回值越小优先级越高
        return 1;
    }
}
```

## Spring MVC

### 说说自己对于 Spring MVC 了解?

​	MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将业务逻辑、数据、显示分离来组织代码。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152220957.png)

​	网上有很多人说 MVC 不是设计模式，只是软件设计规范，我个人更倾向于 MVC 同样是众多设计模式中的一种。**[java-design-patterns](https://github.com/iluwatar/java-design-patterns)** 项目中就有关于 MVC 的相关介绍。

​	想要真正理解 Spring MVC，我们先来看看 Model 1 和 Model 2 这两个没有 Spring MVC 的时代。

​	**Model 1 时代**

​	很多学 Java 后端比较晚的朋友可能并没有接触过 Model 1 时代下的 JavaWeb 应用开发。在 Model1 模式下，整个 Web 应用几乎**全部用 JSP 页面**组成，只用少量的 JavaBean 来处理数据库连接、访问等操作。

​	这个模式下 JSP 即是控制层（Controller）又是表现层（View）。显而易见，这种模式存在很多问题。比如控制逻辑和表现逻辑混杂在一起，导致**代码重用率极低**；再比如前端和后端相互依赖，难以进行测试维护并且开发效率极低。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152221672.png)

​	**Model 2 时代**

​	学过 Servlet 并做过相关 Demo 的朋友应该了解“Java Bean(Model)+ JSP（View）+Servlet（Controller） ”这种开发模式，这就是早期的 JavaWeb MVC 开发模式。

- Model:系统涉及的数据，也就是 dao 和 bean。
- View：展示模型中的数据，只是用来展示。
- Controller：处理用户请求都发送给 ，返回数据给 JSP 并展示给用户。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152221914.png)

​	Model2 模式下还存在很多问题，Model2 的**抽象和封装程度还远远不够**，使用 Model2 进行开发时<u>不可避免地会重复造轮子</u>，这就大大降低了程序的可维护性和复用性。于是，很多 JavaWeb 开发相关的 MVC 框架应运而生比如 Struts2，但是 Struts2 比较笨重。

​	**Spring MVC 时代**

​	随着 Spring 轻量级开发框架的流行，Spring 生态圈出现了 Spring MVC 框架， Spring MVC 是当前最优秀的 MVC 框架。相比于 Struts2 ， Spring MVC 使用更加简单和方便，开发效率更高，并且 Spring MVC 运行速度更快。

​	**MVC 是一种设计模式，Spring MVC 是一款很优秀的 MVC 框架。**Spring MVC 可以帮助我们进行更简洁的 Web 层的开发，并且它天生与 Spring 框架集成。Spring MVC 下我们一般把后端项目分为 Service 层（处理业务）、Dao 层（数据库操作）、Entity 层（实体类）、Controller 层(控制层，返回数据给前台页面)。

### Spring MVC 的核心组件有哪些？

记住了下面这些组件，也就记住了 SpringMVC 的工作原理。

- **`DispatcherServlet`** ：**核心的<u>中央处理器</u>**，负责接收请求、分发，并给予客户端响应。
- **`HandlerMapping`** ：**处理器映射器**，根据 uri 去匹配查找能处理的 `Handler` ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
- **`HandlerAdapter`** ：**处理器适配器**，根据 `HandlerMapping` 找到的 `Handler` ，适配执行对应的 `Handler`；
- **`Handler`** ：**请求处理器**，处理实际请求的处理器。
- **`ViewResolver`** ：**视图解析器**，根据 `Handler` 返回的逻辑视图 / 视图，解析并渲染真正的视图，并传递给 `DispatcherServlet` 响应客户端

### SpringMVC 工作原理了解吗?

​	**Spring MVC 原理如下图所示：**

> SpringMVC 工作原理的图解我没有自己画，直接图省事在网上找了一个非常清晰直观的，原出处不明。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202209152223358.png)

**流程说明（重要）：**

1. 客户端（浏览器）发送请求， `DispatcherServlet`**拦截请求**。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据 uri 去匹配查找能处理的 `Handler`（也就是我们平常说的 `Controller` 控制器） ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
3. `DispatcherServlet` 调用 `HandlerAdapter`**适配执行** `Handler` 。
4. `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象给`DispatcherServlet`，`ModelAndView` 顾名思义，包含了**数据模型**以及相应的**视图的信息**。`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
5. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
6. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
7. 把 `View` 返回给请求者（浏览器）

### 统一异常处理怎么做？

​	推荐使用注解的方式统一异常处理，具体会使用到 `@ControllerAdvice` + `@ExceptionHandler` 这两个注解 。

```java
@ControllerAdvice
@ResponseBody
public class GlobalExceptionHandler {

    @ExceptionHandler(BaseException.class)
    public ResponseEntity<?> handleAppException(BaseException ex, HttpServletRequest request) {
      //......
    }

    @ExceptionHandler(value = ResourceNotFoundException.class)
    public ResponseEntity<ErrorReponse> handleResourceNotFoundException(ResourceNotFoundException ex, HttpServletRequest request) {
      //......
    }
}
```

​	这种异常处理方式下，会给所有或者指定的 `Controller` 织入异常处理的逻辑（AOP），当 `Controller` 中的方法**抛出异常的时候**，由被`@ExceptionHandler` 注解修饰的方法进行处理。

​	`ExceptionHandlerMethodResolver` 中 `getMappedMethod` 方法决定了异常具体被哪个被 `@ExceptionHandler` 注解修饰的方法处理异常。

```java
@Nullable
private Method getMappedMethod(Class<? extends Throwable> exceptionType) {
    List<Class<? extends Throwable>> matches = new ArrayList<>();
    //找到可以处理的所有异常信息。mappedMethods 中存放了异常和处理异常的方法的对应关系
    for (Class<? extends Throwable> mappedException : this.mappedMethods.keySet()) {
        if (mappedException.isAssignableFrom(exceptionType)) {
            matches.add(mappedException);
        }
    }
    // 不为空说明有方法处理异常
    if (!matches.isEmpty()) {
        // 按照匹配程度从小到大排序
        matches.sort(new ExceptionDepthComparator(exceptionType));
        // 返回处理异常的方法
        return this.mappedMethods.get(matches.get(0));
    }
    else {
        return null;
    }
}
```

​	从源代码看出： **`getMappedMethod()`会首先找到可以匹配处理异常的所有方法信息，然后对其进行从小到大的排序，最后取最小的那一个匹配的方法(即匹配度最高的那个)。**

## Spring Data JPA

> 又参考了[ jpa详解_java菜鸟1的博客-CSDN博客_jpa](https://blog.csdn.net/qq_51308214/article/details/125165747)

​	JPA（Java Persistence API）和JDBC类似，也是官方定义的一组接口，但是它相比传统的JDBC，它是为了实现ORM而生的，即Object-Relationl Mapping，它的作用是**在关系型数据库和对象之间形成一个映射**，这样，我们在具体的操作数据库的时候，就<u>不需要再去和复杂的SQL语句</u>打交道，只要像平时操作对象一样操作它就可以了。


### 如何使用 JPA 在数据库中非持久化一个字段？

假如我们有下面一个类：

```java
@Entity(name="USER")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "ID")
    private Long id;

    @Column(name="USER_NAME")
    private String userName;

    @Column(name="PASSWORD")
    private String password;

    private String secrect;

}
```

​	如果我们想让`secrect` 这个字段不被持久化，也就是不被数据库存储怎么办？我们可以采用下面几种方法：

```java
static String transient1; // not persistent because of static
final String transient2 = "Satish"; // not persistent because of final
transient String transient3; // not persistent because of transient
@Transient
String transient4; // not persistent because of @Transient
```

​	一般使用后面两种方式比较多，我个人使用注解的方式比较多。

### JPA 的审计功能是做什么的？有什么用？

​	审计功能主要是帮助我们记录数据库操作的**具体行为**比如某条记录是谁创建的、什么时间创建的、最后修改人是谁、最后修改时间是什么时候。

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@MappedSuperclass
@EntityListeners(value = AuditingEntityListener.class)
public abstract class AbstractAuditBase {

    @CreatedDate
    @Column(updatable = false)
    @JsonIgnore
    private Instant createdAt;

    @LastModifiedDate
    @JsonIgnore
    private Instant updatedAt;

    @CreatedBy
    @Column(updatable = false)
    @JsonIgnore
    private String createdBy;

    @LastModifiedBy
    @JsonIgnore
    private String updatedBy;
}
```

- `@CreatedDate`: 表示该字段为创建时间字段，在这个实体被 insert 的时候，会设置值

- `@CreatedBy` :表示该字段为创建人，在这个实体被 insert 的时候，会设置值

  `@LastModifiedDate`、`@LastModifiedBy`同理。

### 实体之间的关联关系注解有哪些？

- `@OneToOne `: 一对一。
- `@ManyToMany` ：多对多。
- `@OneToMany` : 一对多。
- `@ManyToOne` ：多对一。

利用 `@ManyToOne` 和 `@OneToMany` 也可以表达多对多的关联关系

## 参考

- 《Spring 技术内幕》
- 《从零开始深入学习 Spring》：https://juejin.cn/book/6857911863016390663
- [http://www.cnblogs.com/wmyskxz/p/8820371.html](http://www.cnblogs.com/wmyskxz/p/8820371.html)
- [https://www.journaldev.com/2696/spring-interview-questions-and-answers](https://www.journaldev.com/2696/spring-interview-questions-and-answers)
- [https://www.edureka.co/blog/interview-questions/spring-interview-questions/](https://www.edureka.co/blog/interview-questions/spring-interview-questions/)
- https://www.cnblogs.com/clwydjgs/p/9317849.html
- [https://howtodoinjava.com/interview-questions/top-spring-interview-questions-with-answers/](https://howtodoinjava.com/interview-questions/top-spring-interview-questions-with-answers/)
- [http://www.tomaszezula.com/2014/02/09/spring-series-part-5-component-vs-bean/](http://www.tomaszezula.com/2014/02/09/spring-series-part-5-component-vs-bean/)
- https://stackoverflow.com/questions/34172888/difference-between-bean-and-autowired

# 注解参考

[Spring&SpringBoot常用注解总结 | JavaGuide](https://javaguide.cn/system-design/framework/spring/spring-common-annotations.html#_0-前言)