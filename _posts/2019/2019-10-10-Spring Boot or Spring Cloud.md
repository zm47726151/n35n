## Spring Boot/Spring Cloud

### 什么是 spring boot？

在Spring框架这个大家族中，产生了很多衍生框架，比如 Spring、SpringMvc框架等，Spring的核心内容在于控制反转(IOC)和依赖注入(DI),所谓控制反转并非是一种技术，而是一种思想，在操作方面是指在spring配置文件中创建，依赖注入即为由spring容器为应用程序的某个对象提供资源，比如 引用对象、常量数据等。

SpringBoot是一个框架，一种全新的编程规范，他的产生简化了框架的使用，所谓简化是指简化了Spring众多框架中所需的大量且繁琐的配置文件，所以 SpringBoot是一个服务于框架的框架，服务范围是简化配置文件。

### 为什么要用 spring boot？

- Spring Boot使编码变简单

- Spring Boot使配置变简单

- Spring Boot使部署变简单

- Spring Boot使监控变简单

- 解决了Spring的不足

### spring boot 核心配置文件是什么？

Spring Boot提供了两种常用的配置文件：

- properties文件

- yml文件

### spring boot 配置文件有哪几种类型？它们有什么区别？

Spring Boot提供了两种常用的配置文件，分别是properties文件和yml文件。

相对于properties文件而言，yml文件更年轻，也有很多的坑。可谓成也萧何败萧何，yml通过空格来确定层级关系，使配置文件结构跟清晰，但也会因为微不足道的空格而破坏了层级关系。

### Spring Boot的主要特性：

- （1）遵循“习惯优于配置”的原则，使用Spring Boot只需要很少的配置，大部分的时候我们直接使用默认的配置即可； 

- （2）项目快速搭建，可以无需配置的自动整合第三方的框架； 

- （3）可以完全不使用XML配置文件，只需要自动配置和Java Config； 

- （4）内嵌Servlet容器，降低了对环境的要求，可以使用命令直接执行项目，应用可用jar包执行：java -jar； 

- （5）提供了starter POM, 能够非常方便的进行包管理, 很大程度上减少了jar hell或者dependency hell； 

- （6）运行中应用状态的监控； 

- （7）对主流开发框架的无配置集成； 

- （8）与云计算的天然继承；

### Spring Boot的核心功能：

**（1）独立运行的Spring项目**

- Spring Boot可以以jar包的形式进行独立的运行，使用：java -jar xx.jar 就可以成功的运行项目，或者在应用项目的主程序中运行main函数即可；

**（2）内嵌的Servlet容器 **

内嵌容器，使得我们可以执行运行项目的主程序main函数，是想项目的快速运行；

主程序代码SpringbootDemoApplication.java

```java

package com.ceshi.demo;
 
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
 
@SpringBootApplication
public class SpringbootDemoApplication {
 
    public static void main(String[] args) {
        SpringApplication.run(SpringbootDemoApplication.class, args);
    }
}


```
**（3）提供starter简化Manen配置 **

Spring Boot提供了一系列的starter pom用来简化我们的Maven依赖

[可参考官网](https://docs.spring.io/spring-boot/docs/1.4.1.RELEASE/reference/htmlsingle/#using-boot-starter)

**（4）自动配置Spring **

Spring Boot会根据我们项目中类路径的jar包/类，为jar包的类进行自动配置Bean，这样一来就大大的简化了我们的配置。当然，这只是Spring考虑到的大多数的使用场景，在一些特殊情况，我们还需要自定义自动配置；

**（5）应用监控 **

Spring Boot提供了基于http、ssh、telnet对运行时的项目进行监控

**（6）无代码生成和XML配置 **

Spring Boot神奇的地方不是借助于代码生成来实现的，而是通过条件注解的方式来实现的，这也是Spring 4.x的新特性。


### spring boot 有哪些方式可以实现热部署？

SpringBoot热部署实现有两种方式：

①. 使用spring loaded

在项目中添加如下代码：

```xml

<build>
        <plugins>
            <plugin>
                <!-- springBoot编译插件-->
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <dependencies>
                    <!-- spring热部署 -->
                    <!-- 该依赖在此处下载不下来，可以放置在build标签外部下载完成后再粘贴进plugin中 -->
                    <dependency>
                        <groupId>org.springframework</groupId>
                        <artifactId>springloaded</artifactId>
                        <version>1.2.6.RELEASE</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>

```

②. 使用spring-boot-devtools

在项目的pom文件中添加依赖：

```xml

<!--热部署jar-->
 <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-devtools</artifactId>
 </dependency>

```


### jpa 和 hibernate 有什么区别？

JPA Java Persistence API，是Java EE 5的标准ORM接口，也是ejb3规范的一部分。

Hibernate，当今很流行的ORM框架，是JPA的一个实现，但是其功能是JPA的超集。

JPA和Hibernate之间的关系，可以简单的理解为JPA是标准接口，Hibernate是实现。那么Hibernate是如何实现与JPA的这种关系的呢。Hibernate主要是通过三个组件来实现的，及hibernate-annotation、hibernate-entitymanager和hibernate-core。

ibernate-annotation是Hibernate支持annotation方式配置的基础，它包括了标准的JPA annotation以及Hibernate自身特殊功能的annotation。

hibernate-core是Hibernate的核心实现，提供了Hibernate所有的核心功能。

hibernate-entitymanager实现了标准的JPA，可以把它看成hibernate-core和JPA之间的适配器，它并不直接提供ORM的功能，而是对hibernate-core进行封装，使得Hibernate符合JPA的规范。

### 什么是 spring cloud？

从字面理解，Spring Cloud 就是致力于分布式系统、云服务的框架。

Spring Cloud 是整个 Spring 家族中新的成员，是最近云服务火爆的必然产物。

Spring Cloud 为开发人员提供了快速构建分布式系统中一些常见模式的工具，例如：

配置管理、服务注册与发现、断路由、智能路由、服务间调用、负载均衡、微代理、控制总线、一次性令牌、全局锁、领导选举、分布式会话、集群状态、分布式消息等等，使用 Spring Cloud 开发人员可以开箱即用的实现这些模式的服务和应用程序。这些服务可以任何环境下运行，包括分布式环境，也包括开发人员自己的笔记本电脑以及各种托管平台。

### spring cloud 断路器的作用是什么？

在Spring Cloud中使用了Hystrix 来实现断路器的功能，断路器可以防止一个应用程序多次试图执行一个操作，即很可能失败，允许它继续而不等待故障恢复或者浪费 CPU 周期，而它确定该故障是持久的。断路器模式也使应用程序能够检测故障是否已经解决，如果问题似乎已经得到纠正，应用程序可以尝试调用操作。

断路器增加了稳定性和灵活性，以一个系统，提供稳定性，而系统从故障中恢复，并尽量减少此故障的对性能的影响。它可以帮助快速地拒绝对一个操作，即很可能失败，而不是等待操作超时（或者不返回）的请求，以保持系统的响应时间。如果断路器提高每次改变状态的时间的事件，该信息可以被用来监测由断路器保护系统的部件的健康状况，或以提醒管理员当断路器跳闸，以在打开状态。

### spring cloud 的核心组件有哪些？

①. 服务发现——Netflix Eureka

一个RESTful服务，用来定位运行在AWS地区（Region）中的中间层服务。由两个组件组成：Eureka服务器和Eureka客户端。Eureka服务器用作服务注册服务器。Eureka客户端是一个java客户端，用来简化与服务器的交互、作为轮询负载均衡器，并提供服务的故障切换支持。Netflix在其生产环境中使用的是另外的客户端，它提供基于流量、资源利用率以及出错状态的加权负载均衡。

②. 客服端负载均衡——Netflix Ribbon

Ribbon，主要提供客户侧的软件负载均衡算法。Ribbon客户端组件提供一系列完善的配置选项，比如连接超时、重试、重试算法等。Ribbon内置可插拔、可定制的负载均衡组件。

③. 断路器——Netflix Hystrix

断路器可以防止一个应用程序多次试图执行一个操作，即很可能失败，允许它继续而不等待故障恢复或者浪费 CPU 周期，而它确定该故障是持久的。断路器模式也使应用程序能够检测故障是否已经解决。如果问题似乎已经得到纠正，应用程序可以尝试调用操作。

④. 服务网关——Netflix Zuul

类似nginx，反向代理的功能，不过netflix自己增加了一些配合其他组件的特性。

⑤. 分布式配置——Spring Cloud Config

这个还是静态的，得配合Spring Cloud Bus实现动态的配置更新。


### Spring Cloud与DUBBO进行对比

|微服务需要的功能|Dubbo|Spring Cloud|
|--|--|--|
|服务注册和发现|Zookeeper	|Eureka|
|服务调用方式|RPC|RESTful API|
|断路器|有|有|
|负载均衡|有|有|
|服务路由和过滤|有|有|
|分布式配置|无|有|
|分布式锁|无|计划开发|
|集群选主|无|有|
|分布式消息|无|有|

### 为什么选择使用Spring Cloud而放弃了Dubbo

可能大家会问，为什么选择了使用Dubbo之后，而又选择全面使用Spring Cloud呢？其中有几个原因：

1）从两个公司的背景来谈：Dubbo，是阿里巴巴服务化治理的核心框架，并被广泛应用于中国各互联网公司；Spring Cloud是大名鼎鼎的Spring家族的产品。阿里巴巴是一个商业公司，虽然也开源了很多的顶级的项目，但从整体战略上来讲，仍然是服务于自身的业务为主。Spring专注于企业级开源框架的研发，不论是在中国还是在世界上使用都非常广泛，开发出通用、开源、稳健的开源框架就是他们的主业。

2）从社区活跃度这个角度来对比，Dubbo虽然也是一个非常优秀的服务治理框架，并且在服务治理、灰度发布、流量分发这方面做的比Spring Cloud还好，除过当当网在基础上增加了rest支持外，已有两年多的时间几乎都没有任何更新了。在使用过程中出现问题，提交到github的Issue也少有回复。

相反Spring Cloud自从发展到现在，仍然在不断的高速发展，从github上提交代码的频度和发布版本的时间间隔就可以看出，现在Spring Cloud即将发布2.0版本，到了后期会更加完善和稳定。

3) 从整个大的平台架构来讲，dubbo框架只是专注于服务之间的治理，如果我们需要使用配置中心、分布式跟踪这些内容都需要自己去集成，这样无形中使用dubbo的难度就会增加。Spring Cloud几乎考虑了服务治理的方方面面，更有Spring Boot这个大将的支持，开发起来非常的便利和简单。

4）从技术发展的角度来讲，Dubbo刚出来的那会技术理念还是非常先进，解决了各大互联网公司服务治理的问题，中国的各中小公司也从中受益不少。经过了这么多年的发展，互联网行业也是涌现了更多先进的技术和理念，Dubbo一直停滞不前，自然有些掉队，有时候我个人也会感到有点可惜，如果Dubbo一直沿着当初的那个路线发展，并且延伸到周边，今天可能又是另一番景象了。

Spring 推出Spring Boot/Cloud也是因为自身的很多原因。Spring最初推崇的轻量级框架，随着不断的发展也越来越庞大，随着集成项目越来越多，配置文件也越来越混乱，慢慢的背离最初的理念。随着这么多年的发展，微服务、分布式链路跟踪等更多新的技术理念的出现，Spring急需一款框架来改善以前的开发模式，因此才会出现Spring Boot/Cloud项目，我们现在访问Spring官网，会发现Spring Boot和Spring Cloud已经放到首页最重点突出的三个项目中的前两个，可见Spring对这两个框架的重视程度。

总结一下，dubbo曾经确实很牛逼，但是Spring Cloud是站在近些年技术发展之上进行开发，因此更具技术代表性。
