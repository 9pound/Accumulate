# SpringCloud概述

微服务与单体架构的本质区别在于单体架构只有一台服务器而微服务有多台服务器，spring-cloud是一些技术的集合这些技术用来解决像配置管理，服务的注册与发现、负载均衡、断路器、数据监控，异步消息处理

### Spring Cloud Netflix 第一代

- `Netflix Eureka`：一个基于 Rest 服务的服务治理组件，包括服务注册中心、服务注册与服务发现机制的实现，实现了云端负载均衡和中间层服务器的故障转移。
- `Netflix Ribbon`：客户端负载均衡的服务调用组件。
- `Netflix Hystrix`：容错管理工具，实现[断路器](https://www.zhihu.com/search?q=断路器&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A110249846})模式，通过控制服务的节点，从而对延迟和故障提供更强大的容错能力。
- `Netflix Feign`：基于 Ribbon 和 Hystrix 的声明式服务调用组件。
- `Netflix Zuul`：微服务网关，提供动态路由，访问过滤等服务。
- `Netflix Archaius`：配置管理 API，包含一系列配置管理 API，提供动态类型化属性、线程安全配置操作、轮询框架、回调机制等功能。

### Spring Cloud Alibaba 第二代

- `Nacos`：阿里巴巴开源产品，一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。
- `Sentinel`：面向分布式服务架构的轻量级流量控制产品，把流量作为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。
- `RocketMQ`：一款开源的分布式消息系统，基于高可用[分布式集群技术](https://www.zhihu.com/search?q=分布式集群技术&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A110249846})，提供低延时的、高可靠的消息发布与订阅服务。
- `Dubbo`：Apache Dubbo™ 是一款高性能 Java RPC 框架，用于实现服务通信。
- `Seata`：阿里巴巴开源产品，一个易于使用的高性能微服务分布式事务解决方案。

- `Alibaba Cloud ACM`：一款在[分布式架构](https://www.zhihu.com/search?q=分布式架构&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A110249846})环境中对应用配置进行集中管理和推送的应用配置中心产品。
- `Alibaba Cloud OSS`：阿里云对象存储服务（Object Storage Service，简称 OSS），是阿里云提供的海量、安全、低成本、高可靠的云存储服务。您可以在任何应用、任何时间、任何地点存储和访问任意类型的数据。
- `Alibaba Cloud SchedulerX`：阿里中间件团队开发的一款分布式任务调度产品，提供秒级、精准、高可靠、高可用的定时（基于 Cron 表达式）任务调度服务。
- `Alibaba Cloud SMS`：覆盖全球的短信服务，友好、高效、智能的互联化通讯能力，帮助企业迅速搭建客户触达通道。



















#### Config

SpringCloud 通过集中式服务来处理应用程序配置数据管理

程序的配置与部署的微服务完全分离

#### Eureka

三个角色

服务注册

服务续约

获取注册列表信息

服务下线

服务剔除

与zookeeper的区别 AP，CP

```
@EnableDiscoveryClient



server:
  port: 10087 # 端口
spring:
  application:
    name: eureka-server # 应用名称，会在Eureka中显示
eureka:
    server:
        enable-self-preservation: false # 关闭自我保护模式（缺省为打开）
        eviction-interval-timer-in-ms: 1000 # 扫描失效服务的间隔时间（缺省为60*1000ms）
    instance:
      lease-expiration-duration-in-seconds: 10 # 10秒即过期
      lease-renewal-interval-in-seconds: 5 # 5秒一次心跳	
    client:
      service-url: # 配置其他Eureka服务的地址，而不是自己，比如10087
      	defaultZone: http://127.0.0.1:10086/eureka,http://127.0.0.1:10087/eureka
```

#### Ribbon

消费者端负载均衡

与nginx的区别，nginx服务端负载均衡，nginx接受请求然后再转发进行负载均衡

常见负载均衡算法

```
user-service:
  ribbon:
    ConnectTimeout: 250 # Ribbon的连接超时时间
    ReadTimeout: 1000 # Ribbon的数据读取超时时间
    OkToRetryOnAllOperations: true # 是否对所有操作都进行重试
    MaxAutoRetriesNextServer: 1 # 切换实例的重试次数
    MaxAutoRetries: 1 # 对当前实例的重试次数
```

### Feign

Feign中本身已经集成了Ribbon依赖和自动配置

Feign默认也有对Hystix的集成：

```
@FeignClient("user-service")
@EnableFeignClients 

user-service:
  ribbon:
    ConnectTimeout: 250 # 连接超时时间(ms)
    ReadTimeout: 1000 # 通信超时时间(ms)
    OkToRetryOnAllOperations: true # 是否对所有操作重试
    MaxAutoRetriesNextServer: 1 # 同一服务不同实例的重试次数
    MaxAutoRetries: 1 # 同一实例的重试次数
  hystrix:
    enabled: true # 开启Feign的熔断功能
  compression:
    request:
      enabled: true # 开启请求压缩
      mime-types: text/html,application/xml,application/json # 设置压缩的数据类型
      min-request-size: 2048 # 设置触发压缩的大小下限
    response:
      enabled: true # 开启响应压缩
```



#### Hystrix

```
 @HystrixCommand(fallbackMethod = "queryUserByIdFallback")
```



#### Zuul



过滤器

```
@EnableZuulProxy 

zuul:
  routes:
    user-service: # 这里是路由id，随意写
      path: /user-service/** # 这里是映射路径
      serviceId: user-service # 指定服务名称 
      
zuul:
  routes:
    user-service: /user-service/** # 这里是映射路径
```

#### Stream

#### Sleuth

#### Security





@EnableCircuitBreaker

@EnableEurekaClient



