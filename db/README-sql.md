#### 查询

1. 简单查询
2. 复杂查询：简单子查询==subquery、派生表(在from子句中的子查询)==derived、UNION查询
### SQL

#### 基本sql

1. show databases;	查看所有的库  

2. use 库名;	使用xxx库

3. show create table 表名;查看表结构

4. drop table 表名; 删除表

5. truncate table 表名; 清空表数据

6. SHOW STATUS  查询sql服务器状态，可以通过like 'xx'查询多个

   [对应枚举值](https://www.mysqlzh.com/doc/40/413.html)

7. show  VARIABLES 查询服务器的配置

8. SHOW FULL PROCESSLIST 查看数据库所有连接

9. kill id	杀死某个连接

10.	SHOW GRANTS	查看用户的权限

11. select version()	查看mysql的版本

12. select * from mysql.user 查看所有用户

#### 控制流程函数

1. 	CASE 
	WHEN ... THEN xxx
	WHEN ... THEN xxx
	....
	ELSE xxx 
	END 
	
	例子：CASE WHEN name='xx' then true ELSE false AS author 判断name是否是xx 

	
#### 关联

1. left join 左关联

   > select * from a left join b on ...

   左关联b表查询a表,生成的是a、b表的所有列的表,数据为a表所有数据+符合条件的关联上的b表的列,不符合条件的使用的为null来展示

2. inner join 内关联

   结果为2个表的交集
   
3. union	合并查询

	> 每个 SELECT 语句必须拥有相同数量的列
	
	> 列也必须拥有相似的数据类型
	
	> 列的顺序必须相同

UNION ALL允许重复的值

#### 函数

1. DATEDIFF
	
	计算datetime类型的值与现在的天数差(不会看后面的具体小时)

### 实用功能

#### 方便插入数据

1. 建表是加上特定的语句：ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t';
```sql
CREATE TABLE `table1` (
  `year` VARCHAR(4),
  `month` VARCHAR(10),
  )ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t';
```

表示使用\t分隔数据

2. 使用txt文档保存数据，使用[tab]符号来分隔数据

3. load data local inpath '/usr/lib/data/data.txt' into table table1; 插入数据

#### 查看执行sql的计划

	使用EXPLAIN字段添加在sql前面，查看执行计划。方便优化sql
	
	返回列的含义：
	
	> id	
	> select_type 查询类型(SIMPLE、DERIVED、SUBQUERY、UNION、UNION RESULT、DEPENDENT、UNCACHEABLE)
	> table 访问表名 
	> type	访问类型(ALL、index、range、const, system)

-	id:如果有一行前面有大id的行，暗示这一行会在后面执行(例如需要依赖外层查询)
-	table:如果是<derived3>、<union1,4>这种临时表，表示使用了id为x的结果
-	ALL全表扫描，但如果有limit或者extra中有Using distinct/not exists也不是全表扫描
-	range有限制的索引扫描，一般是sql带有between、where中带有>

### 优化

1. group by  + having

	分组后,可使用having过滤


2. 查询：速度char>varchar>text

3. 尽量保证where使用了索引,不使用索引会进行全表扫描

	1. 在where句不要对字段进行null判断,也就保证一些字段不要为null

	2. where尽量避免使用!= < > 	
	
	3. 使用or来连接条件，如果有一个没有索引,也会导致扫描全表
		
		可以使用 union(其实就是合并多个select)
	
	4. in和not in 也会导致全表扫描
	
		连续的使用 between
		
	5. like xxx也会导致全表扫描
	
		可以使用全文检索
		
	6. where使用函数操作，会导致全表扫描
	
4. 性能

	1. update,只改1、2个字段，不要update全部
	
	2. 大数据表(几百)join,先分页(limit)再join
	
	3. 尽量使用数字型字段,查询时字符串会逐个比较字符
	
	4. 不使用select *,使用具体的字段代替
	

### 链接

- [高性能MySql]	
