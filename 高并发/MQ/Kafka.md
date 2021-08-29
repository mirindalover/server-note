### Kafka

消息引擎，同时也具备流处理的能力(Kafka Streams)

消息系统需要解决的点：1、消息的格式(xml、json)	2、消息传输协议(点对点模型、发布订阅模型)

Kafka的消息格式：二进制

遵循了JMS规范

为什幺要消息引擎：削峰、低耦合

#### Kafka消息架构

Kafka消息架构：主题、分区、副本。一个主题可以配置M个分区，每个分区可以配置N个副本；

Kafka的副本：Leader、Follower副本;生产者向Leader副本写消息，消费者从Leader副本读消息。Follower副本只是向Leader发请求，让Leader把新消息发送给它

Kafka的分区：生产者把一条消息发送到一个分区中，每条消息在分区的位置由Offset来表示(从0开始)

#### Kafka持久化数据

使用Log来保存数据，追加写的方式，提高写数据的性能，从而提高高吞吐量

Log通过日志段的方式：写满一个日志段后，切分出一个新的日志段，把老的保存

Kafka后台有定时任务检查日志段能否删除


#### Kafka的几个版本

Apache Kafka：最基本的版本。connect只有一种、没有监控(可以使用其他监控，如Kafaka Manager)

Confluent Kafka：Schema注册中心、REST proxy(通过http访问kafka)。企业版有跨数据中心备份、集群监控

CDH/HDP Kakfa：所有操作都在控制台，包括 安装、运维、管理、监控

稳定版本：0.11.0.3(消息引擎比较完善)



