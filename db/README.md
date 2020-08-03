### 数据库分类

#### 关系型数据库

MySQL、Oracle、DB2、Microsoft SQL Server、Microsoft Access

ACID(原子性、一致性、隔离性、持久性)

#### 非关系型数据库(NoSQL)

1. 键值(Key-Value)存储数据库： Redis。解决关系型数据库无法存储数据结构(如无法存储关注列表)
2. 列存储数据库：HBase
3. 文档型数据库：MongoDb
4. 图形(Graph)数据库：Neo4J

> 不保证关系数据的ACID特性。易扩展、大数据量，高性能

#### 类SQL数据库-Hive

Hive是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射成一张表，并提供类sql语句的查询功能

Hive使用Hql作为查询接口，使用HDFS存储，使用mapreduce计算

Hive的本质是将Hql转化为mapreduce

#### Hive和关系型数据库的区别

1. 数据库的查询语句为SQL，Hive的查询语句为HQL

2. 数据库数据存储在LocalFS，Hive的数据存储在HDFS

3. Hive执行MapReduce，MySQL执行Executor

4. Hive没有索引

5. Hive延迟性高

6. Hive可扩展性高

7. Hive数据规模大