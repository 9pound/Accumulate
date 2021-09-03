# SpringCloud概述

微服务与单体架构的本质区别在于单体架构只有一台服务器而微服务有多台服务器，spring-cloud是一些技术的集合这些技术用来解决像配置管理，服务的注册与发现、负载均衡、断路器、数据监控，异步消息处理



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