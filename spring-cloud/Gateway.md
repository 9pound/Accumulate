# Spring Cloud Gateway

为什么需要网关



在微服务当中、客户端需要知道机器的具体IP或者域名URL、服务众多时、这是非常难得记忆的



网关具有身份认证与安全、审查与监控、动态路由、负载均衡、缓存、请求分片与管理、静态响应处理等功能。当然最主要的职责还是与“外界联系”。



作用：

- 鉴权、限流、熔断、日志
- 协议转换
- 请求转发
- 统一错误处理





核心概念

- 路由：由一组断言和一组过滤器组成
- 断言：允许开发者去定义匹配来自于 Http Request 中的任何信息，
- 过滤器：Gateway Filter 和 Global Filter。过滤器将会对请求和响应进行处理。







动态路由

- 整合eureka实现动态路由
- 整合nacos实现动态路由







rpc 与http的区别？

