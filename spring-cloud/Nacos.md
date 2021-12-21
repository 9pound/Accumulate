# Nacos

注册中心：类似于目录服务的作用、主要用来存储服务信息、URL、路由信息

服务注册和服务发现



为什么要注册中心

- 服务注册后，如何被及时发现
- 服务宕机后，如何及时下线
- 服务如何有效的水平扩展
- 服务发现时，如何进行路由
- 服务异常时，如何进行降级
- 注册中心如何实现自身的高可用







配置中心



1、nocas 上新建配置

```properties
${prefix}-${spring.profile.active}.${file-extension}
```

- `prefix` 默认为 `spring.application.name` 的值，也可以通过配置项 `spring.cloud.nacos.config.prefix`来配置。
- `spring.profile.active` 即为当前环境对应的 profile。**注意：当 `spring.profile.active` 为空时，对应的[连接符](https://www.zhihu.com/search?q=连接符&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A148658996}) `-` 也将不存在，dataId 的拼接格式将变成 `${prefix}.${file-extension}`**
- `file-exetension` 为配置内容的数据格式，可以通过配置项 `spring.cloud.nacos.config.file-extension` 来配置。目前只支持 `properties` 和 `yaml` 类型，默认为 `properties`。

2、然后使用@Value注解注入配置即可

@RefreshScope ：类上注解 实现配置的自动更新

3、配置项中开启配置中心

```text
spring:
  application:
    name: product-service # 应用名称
  cloud:
    nacos:
      config:
        enabled: true # 如果不想使用 Nacos 进行配置管理，设置为 false 即可
        server-addr: 127.0.0.1:8848 # Nacos Server 地址
        group: DEFAULT_GROUP # 组，默认为 DEFAULT_GROUP
        file-extension: yaml # 配置内容的数据格式，默认为 properties
```





为什么需要配置？

配置变更是调整系统运行时的行为的有效手段。





- `Namespace`：代表不同的**环境**，如：开发、测试， 生产等；
- `Group`：代表某个**项目**，如：XX物流项目，XX教育项目；
- `DataId`：每个项目下往往有若干个**应用**，每个配置集(DataId)是一个应用的**主配置文件**



```text
server:
  port: 7070 # 端口

spring:
  application:
    name: product-service # 应用名称
  cloud:
    nacos:
      config:
        enabled: true # 如果不想使用 Nacos 进行配置管理，设置为 false 即可
        server-addr: 127.0.0.1:8848 # Nacos Server 地址
        group: DEFAULT_GROUP # 组，默认为 DEFAULT_GROUP
        file-extension: yaml # 配置内容的数据格式，默认为 properties
        namespace: 450a3f07-08ee-49f6-8213-9b04b06cd3cc # 对应 dev 环境
```