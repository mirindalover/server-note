## 分布式事务

### TCC(try-confirm-cancel)

> try试试各个服务是否正常

> TCC框架通过事务活动日志记录状态。如果失败会一直循环重试保证cancel成功

### 异步事务

上面TCC是程序同步进行，异步的比如使用MQ。MQ的分布式事务--可靠消息最终一致性方案(可靠消息服务)

<img src="https://github.com/mirindalover/server-note/blob/master/%E5%88%86%E5%B8%83%E5%BC%8F/%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1/resource/message_coherence.png" alt=""/>