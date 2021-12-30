### Docker

[Docker镜像地址](https://hub.docker.com)


#### 基础命令

- 搜索镜像 

```shell
docker search activemq
```

- 安装镜像

```shell
docker pull
```

- 查看已经安装的镜像

```shell
docker images
```

- 启动

```shell
docker run --name [名字] [镜像] 
```

- 查看已经启动的镜像

```shell
docker ps
```

- 进入容器目录

```shell
docker exec -it [容器id] /bin/sh
```

#### 安装Kafka

docker pull wurstmeister/kafka 

docker pull wurstmeister/zookeeper 


- 启动

docker run -d --name zookeeper -p 2181 -t wurstmeister/zookeeper

docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --env KAFKA_ADVERTISED_HOST_NAME=127.0.0.1 --env KAFKA_ADVERTISED_PORT=9092 --volume /etc/localtime:/etc/localtime wurstmeister/kafka:latest  

- 进入Kafka目录

docker ps 查看启动的容器id

docker exec -it [容器id] /bin/sh

#### 安装redis

- 启动

```shell
docker run --name some-redis -d redis
```
- 进入redis

```shell
docker exec -it some-redis /bin/bash

redis-cli 
```

#### 安装clickhouse

https://hub.docker.com/r/clickhouse/clickhouse-server/

根据文档需要启动server
连接需要启动client
