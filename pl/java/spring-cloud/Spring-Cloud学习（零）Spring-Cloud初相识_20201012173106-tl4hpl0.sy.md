# 前言
{: id="20210104083616-lbq9f58"}

本篇文章是学习 Spring Cloud 的开篇文章，主要包括关于 Spring Cloud 一些问题，以及 Spring Cloud 的学习资源整理。
{: id="20210104083616-7lod4r4"}

# 为什么要学习 Spring Cloud
{: id="20210104083616-nw3s1kd"}

第一，程序员就应该不断学习。
{: id="20210104083616-ea8o626"}

作为程序员，要保持对新技术的热情，养成不断学习的好习惯，Spring Cloud 作为当前最主流的 Java 开发技术，包含了许多技术点，包括微服务、分布式、远程服务调用等，这些技术，运用到实际开发中，可以大幅度提升软件的性能。
{: id="20210104083616-ksyjhw1"}

第二，找工作需要。
{: id="20210104083616-s30fml5"}

打开招聘网站，查看招聘 Java 开发岗位的要求，95% 以上都要求掌握 Spring Cloud，从这可以看出，Spring Cloud 已经成为 Java 程序员必须要掌握的知识点，如果不会 Spring Cloud，很难找到好的工作。
{: id="20210104083616-mwiagxp"}

# 什么是 Spring Cloud
{: id="20210104083616-8ha53ni"}

本篇文章是学习 Spring Cloud 的开篇文章，主要包括关于 Spring Cloud 一些问题，以及 Spring Cloud 的学习资源整理。
{: id="20210104083616-wvana82"}

# 为什么要学习 Spring Cloud
{: id="20210104083616-mpx81vn"}

第一，程序员就应该不断学习。
{: id="20210104083616-63q3icx"}

作为程序员，要保持对新技术的热情，养成不断学习的好习惯，Spring Cloud 作为当前最主流的 Java 开发技术，包含了许多技术点，包括微服务、分布式、远程服务调用等，这些技术，运用到实际开发中，可以大幅度提升软件的性能。
{: id="20210104083616-wrtfwqa"}

第二，找工作需要。
{: id="20210104083616-ghnbihw"}

打开招聘网站，查看招聘 Java 开发岗位的要求，95% 以上都要求掌握 Spring Cloud，从这可以看出，Spring Cloud 已经成为 Java 程序员必须要掌握的知识点，如果不会 Spring Cloud，很难找到好的工作。
{: id="20210104083616-utimh8q"}

Spring Cloud 和 Spring Boot 是什么关系
{: id="20210105094809-nz4eg1v"}

Spring cloud 是基于 Spring Boot 来进行开发的，一个 Spring Cloud 项目是由多个 Spring Boot 项目组成的。所以要学习 Spring Cloud 的前提是要会使用 Spring Boot。
{: id="20210105094809-ublhv8e"}

# 什么是 Spring Cloud
{: id="20210104083616-i3n9b53"}

Spring Cloud 是一个开发分布式系统（参考 [分布式、集群、微服务、SOA 之间的区别](https://blog.csdn.net/heatdeath/article/details/79038795)）的工具集，主要包括配置管理、服务注册与发现、控制总线、负载均衡、断路器、智能路由等。它的运用场景模型，如下图所示：
{: id="20210104083616-ypfrhpz"}

![Microservices diagram](https://spring.io/images/diagram-microservices-88e01c7d34c688cb49556435c130d352.svg)
{: id="20210104083616-ski0ppj"}

{: id="20210105094946-sx0lz1m"}

先简单介绍一下 Spring Cloud 的各个组件：
{: id="20210105094945-tmijbpx"}

- {: id="20210105095011-y1aa5ag"}eureka: 服务注册中心，一般在分布式系统中，都会有很多个服务，我们需要一个服务注册中心来管理这些服务。
- {: id="20210105095137-cxrrzma"}ribbon: 负载均衡客户端，在微服务架构中，业务都会被拆分成一个独立的服务，服务与服务的通讯是基于 http restful 的。Spring cloud 有两种服务调用方式，一种是 ribbon+restTemplate，另一种是 feign（默认集成了 ribbon）。
- {: id="20210105100158-6h486a8"}feign: feign 是一个声明式的伪 http 客户端，它使得写 http 客户端变得更简单。使用 feign，只需要创建一个接口并注解。它具有可插拔的注解特性，可使用 feign 注解和 JAX-RS 注解。feign 支持可插拔的编码器和解码器。feign 默认集成了 ribbon，并和 eureka 结合，默认实现了负载均衡的效果。
- {: id="20210105101145-ism5ayx"}hystrix: 断路器，由于网络原因或者自身的原因，服务并不能保证 100% 可用，如果单个服务出现问题，调用这个服务就会出现线程阻塞，此时若有大量的请求涌入，Servlet 容器的线程资源会被消耗完毕，导致服务瘫痪。服务与服务之间的依赖性，故障会传播，会对整个微服务系统造成灾难性的严重后果，这就是服务故障的“雪崩”效应。hystrix 就是用来避免这个问题的，hystrix 可以和 ribbon + RestTemplate 或者是 feign 组合使用。
- {: id="20210105101708-1xrdrs9"}zuul: 智能路由，它的主要功能是路由转发和过滤器。路由功能是微服务的一部分，比如／api/user 转发到到 user 服务，/api/shop 转发到到 shop 服务。zuul 默认和 Ribbon 结合实现了负载均衡的功能。
- {: id="20210105142123-mltpy0e"}config: 在分布式系统中，由于服务数量巨多，为了方便服务配置文件统一管理，实时更新，所以需要分布式配置中心组件。在 Spring Cloud 中，有分布式配置中心组件 spring cloud config ，它支持配置服务放在配置服务的内存中（即本地），也支持放在远程 Git 仓库中。在 spring cloud config 组件中，分两个角色，一是 config server，二是 config client。
- {: id="20210105142206-m9pzn0p"}bus: Spring Cloud Bus 将分布式的节点用轻量的消息代理连接起来。它可以用于广播配置文件的更改或者服务之间的通讯，也可以用于监控。本文要讲述的是用 Spring Cloud Bus 实现通知微服务架构的配置文件的更改。
-
{: id="20210105142452-1vy444g"}
{: id="20210105095006-f02hox3"}

{: id="20210104083616-mlqab2a"}

# Spring Cloud 学习资源
{: id="20210104083616-ri3b6ew"}

网上学习 Spring Cloud 的资源很多，我主要是参考的有：
{: id="20210104083616-ids42w7"}

1. {: id="20210104083616-pl3ddin"}[spring-cloud 官网](https://spring.io/projects/spring-cloud)
2. {: id="20210104083616-s848bjp"}[纯洁的微笑 - Spring Cloud 系列文章](http://www.ityouknow.com/spring-cloud.html)
3. {: id="20210104083616-pmpk99k"}[方志朋 - Spring Cloud 系列文章](https://www.fangzhipeng.com/spring-cloud.html)
4. {: id="20210104083616-3hn8koq"}[猿天地 - Spring Cloud 入门到实战系列教程](http://cxytiandi.com/blog/detail/17470)
5. {: id="20210104164439-lqh0rjr"}[周立的博客](http://www.itmuch.com/spring-cloud/spring-cloud-index/)
6. {: id="20210104151054-f4dzxht"}更多的资源可以参考 [Sring Cloud 中文索引](http://springcloud.fun/)
{: id="20210104083616-htgqbos"}

{: id="20210105092427-he03trm"}
