## 消息中间件rocketmq学习笔记

> rocketmq是阿里基于高可用分布式集群技术，自主研发的消息中间件。即可为分布式应用系统提供异步解耦和削峰填谷的能力，同时也具备互联网应用所需的海量消息堆积、高吞吐、可靠重试等特性，是阿里双十一使用的核心产品。

### 基本情况

- [官方github](https://github.com/apache/rocketmq/tree/master/docs/cn)
- [官方网站](https://rocketmq.apache.org/)
- [可视化插件安装](https://www.cnblogs.com/vipstone/p/11128471.html)
- [部署与技术架构](https://github.com/apache/rocketmq/blob/master/docs/cn/architecture.md)
- [关键机制设计](https://github.com/apache/rocketmq/blob/master/docs/cn/design.md)
- [最佳实践](https://github.com/apache/rocketmq/blob/master/docs/cn/best_practice.md)

### 设计理念

- 基于**主题**(`topic`)的**发布**和**订阅**，核心功能**消息发送**、**消息存储**、**消息消费**。整体设计追求简单和性能。

- `NameServer`对比`zookeeper`有极大的提升。

- 高效的IO存储机制，基于文件顺序读写，**内存映射**机制。

- 容忍设计缺陷，rocketmq自身不保证消息只被消费一次，将重复消费问题交由消费者来设计，即如何保障程序设计的**幂等性**，从而简化rocket的内核使其简单高效。


### 核心概念

![rocketmq_architecture_1.png](/docs/middleware/img/rocketmq_architecture_1.png)
<br>(图片来源: rocket官方github)

- **NameServer**

  NameServer是整个rocket的”大脑“，是rocket的注册中心，须先启动NameServer再启动broker。
  broker在启动时会向所有NameServer注册，生产者在发送消息之前会先从NameServer中获取broker服务器地址列表，
  然后根据**负载均衡**算法选择一台服务器发送消息。需要注意的是，多个Namesrv实例组成集群，**但相互独立**，**没有信息交换**。

- **topic**

  消息主题

- **tag**

  消息标签，消息二级分类，用来进一步区分某个topic下的消息分类。

- **producer**

  消息生产者

- **consumer**

  消息消费者

- **message**

  消息载体


### push模型

- 消息堆积
- 重复消费
- 负载策略
- 延迟消息

### pull模型



### 源码分析
