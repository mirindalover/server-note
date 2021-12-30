## Redis

Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件

### 常用命令

- set	设置key对应的value

>	EX seconds – 设置键key的过期时间，单位时秒
>	PX milliseconds – 设置键key的过期时间，单位时毫秒
>	NX – 只有键key不存在的时候才会设置key的值
>	XX – 只有键key存在的时候才会设置key的值

- del	删除指定的一批keys，如果删除中的某些key不存在，则直接忽略

> 删除 集合 时,复杂度为O(M),M为key中的元素个数

- get	返回`key`的`value`。如果key不存在，返回特殊值`nil`。如果`key`的`value`不是string，就返回错误，因为`GET`只处理string类型的`values`

#### 集合

- sadd	添加一个或多个指定的member元素到集合的 key中.指定的一个或者多个元素member 如果已经在集合key中存在则忽略.如果集合key 不存在，则新建集合key,并添加member元素到集合key中.如果key 的类型不是集合则返回错误	-返回值为成功添加的个数
- srem	在key集合中移除指定的元素. 如果指定的元素不是key集合中的元素则忽略 如果key集合不存在则被视为一个空的集合，该命令返回0.如果key的类型不是一个集合,则返回错误	-返回值为成功移除的个数
- sismember	返回成员 member 是否是存储的集合 key的成员
- SCARD 获取集合的成员数

- SMEMBERS 获取集合所有元素

- pexpire 设置过期时间

- ttl	获取key的有效时间

- sunion 合并集合，也可以做查看集合命令(sunion [key] 即是查看集合)

### 源码

- Redis字符使用SDS(simple dynamic string)，没有直接使用c字符

> c字符没有直接获取长度函数,redis有获取长度命令
>
> 杜绝缓冲溢出,append会检查长度，不够会扩展



### 案例

#### 分布式锁

三要素：安全(互斥)、死锁释放、故障容错

1. 过期时间主动释放
2. 释放时，不能直接del。而要先比较再del(防止超时主动释放导致删除其他进程正在用的锁)
3. 重试时等待一段时间，且大于正常获取锁的时间。可以防止竞争资源时发生死锁

官网方案：RedLock 方案：使用多个redis实例来获取锁，当有n/2+1个实例获取锁成功，才表示获取锁成功

带来的不同操作：

1. 释放锁时：需要给所有的节点发送释放请求
2. 故障恢复：宕机后重启的实例在锁超时范围内不可用即可，保证了不会有其他客户端获取到锁

### 链接

[Redis命令](http://www.redis.cn/documentation.html)
[Redis文档](http://www.redis.cn/documentation.html)
[京东Redis缓存系统](http://wiki.cbpmgt.com/confluence/pages/viewpage.action?pageId=15861929)-只能通过内网打开

[Redis分布式锁](https://redis.io/topics/distlock)、[译文](http://ifeve.com/redis-lock/)
[redis文章推荐](http://kaito-kidd.com/)

