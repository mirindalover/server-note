
#### Spring 事务

使用AOP开启事务时，子线程(内部类)对应的方法不会AOP。粗暴的解决方法：通过service.xxx(service就是自己)


### Spring Cloud

#### 核心组件

- Eureka

  > 微服务架构的注册中心
  
  Client 30s发送一个心跳，30s重新拉取注册服务信息
  
  核心是通过内存来记录所有的注册信息，同时使用多级缓存(ReadOnlyCacheMap(30s后台任务发现ReadWriteCacheMap清空了也会过期它)、ReadWriteCacheMap(注册表更新先过期它,此时读仍可缓存))来提升请求相应
  
  单台Server 没秒处理几百请求，每天千万级请求

- Ribbon

  > 负载均衡

- Feign

  > 服务之间调用

  动态代理的方式，简化服务调用的过程

- Hystrix

  > 隔离、熔断、降级 框架

  每个服务都是一个线程池，不影响其他服务
  
  不建议设置很大的超时时间，这样会导致多个慢请求 打挂某个服务(优化服务的接口相应时间是最主要的)

- Zuul

  > 网关















