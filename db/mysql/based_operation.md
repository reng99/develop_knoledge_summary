## 基本操作

这里整理的是在开发中控制台上经常操作的命令行啦(大小写都可，我这里使用推荐的大写) :blush:

> 创建数据库

`CREATE DATABASE IF NOT EXISTS dbname;`

> 删除数据库

`DROP DATABASE dbname;`

> 列出数据库

`SHOW DATABASES;`

> 选择数据库

`USE dbname;`

> MySQL 数据类型

数值类型 : TINYINT , SMALLINT , MEDIUMINT , INT/INTEGER , BIGINT , FLOAT , DOUBLE , DECIMAL

日期和时间类型 : DATE , TIME , YEAR , DATETIME , TIMESTAMP

字符串类型 : CHAR , VARCHAR , TINYBLOB , TINYTEXT , BLOB , TEXT , MEDIUMBLOG , MEDIUMTEXT , LONGBLOG , LONGTEXT

> 创建数据表

`CREATE TABLE table_name (column_name columntype);`

相关demo :

```bash
CREATE TABLE IF NOT EXISTS `reng` (
  `reng_id` INT UNSIGNED AUTO_INCREMENT,
  `reng_title` VARCHAR(100) NOT NULL,
  `reng_author` VARCHAR(40) NOT NULL,
  `submission_date` DATE,
  PRIMARY KEY (`reng_id`)
) ENGINE = InnoDB DEFAULT CHARSET=utf8;
```
> 删除数据表

`DROP TABLE table_name;`

> 插入数据

```bash
INSERT INTO table_name (field1 , field2 , ... fieldN)
                        VALUES
                        (value1 , value2 , ... valueN);
```

相关demo :

```bash
mysql> INSERT INTO reng
    -> (reng_title , reng_author , submission_date)
    -> VALUES
    -> ("学习mysql" , "嘉明" ,NOW());
```

> 查询数据

语法 ：

```bash
SELECT column_name , column_name
FROM table_name
[WHERE Clause]
[LIMIT N][OFFSET M]
```

说明 ：

查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。

SELECT命令可以读取一条或者多条记录。

你可以使用星号(*)来代替其他字段，SELECT语句会返回表的所有字段数据。

你可以通过使用WHERE语句来包含任何条件。

你可以使用LIMIT属性来设定返回的记录数。

你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。

> WHERE 子句

语法 ：

```bash
SELECT field1 , field2 , ... fieldN FROM table_name1  , table_name2 ...
[WHERE condition1 [AND [OR]] condition2 ...
```

说明 : 

查询语句中你可以使用一个或者多个表，表之间使用逗号`,`分割，并使用WHERE语句来设定查询条件。

你可以在WHERE子句中指定任何合理的条件。

你可以使用AND或OR指定一个或者多个条件。

WHERE子句也可以运用于SQL的DELETE或者UPDATE命令。

WHERE子句类型于程序语言中的if条件，根据MySQL表中的字段来读取指定的数据。

> UPDATE 查询

```bash
UPDATE table_name SET field=new-value1 , field=new-value2
[WHERE Clause]
```
说明 ：

你可以同时更新一个或者多个字段。

你可以在WHERE子句中指定任何条件。

你可以在一个单独表中同时更新数据。

> DELETE 语句

语法 ：

DELETE语句从MySQL数据表中删除数据的通用方法。

```bash
DELETE FROM table_name 
[WHERE Clause]
```

说明 ：

如果没有指定WHERE子句，MySQL表中所有记录将被删除。

你可以在WHERE子句中指定任何条件。

你可以在单个表中一次性删除记录。

> LIKE子句  -- 模糊查询

语法 ：

以下是SQL SELECT语句使用LIKE子句从数据表中读取数据的通用语法:

```bash
SELECT field1 , field2 , ... fieldN
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] field2 = 'somevalue'
```

说明 ：

你可以在WHERE子句中指定任何条件。

你可以在WHERE子句中使用LIKE子句。

你可以使用LIKE子句代替等号`=`。

LIKE通常与`%`一同使用，类似于一个元字符的搜索。

你可以使用AND或者OR指定一个或者多个条件。

你可以在DELETE或UPDATE命令中使用WHERE...LIKE子句来指定条件。

> UNION

描述 ：

UNION操作符用于连接连个以上的SELECT语句的结果组合到一个结果集合中。多个SELECT语句会删除重复的数据。

语法 ：

```bash
SELECT expression1 , expression2 , ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1 , expression2 , ... expression_n
FROM tables
[WHERE condition];
```

说明 ：

expression1 , expression2 , ... expression_n : 要检索的列

tables: 要检索的数据表

WHERE conditions : 可选，检索的条件

DISTINCT : 可选，删除结果集中重复的数据。默认情况下UNION操作符已经删除了重复数据，所以DISTINCT修饰符对结果没有什么影响。

ALL ： 可选，返回所有结果集，包含重复数据。

> 排序

语法 ：

使用sql select语句的ORDER BY子句将查询数据排序后再返回数据：

```bash
SELECT field1 ,field , ... fieldN table_name1 , table_name2 ...
ORDER BY field1 , [field2 ...] [ASC [DESC]]
```

说明 ：

你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。

你可以设定多个字段来排序。

你可以使用ASC 或DESC关键字来设置查询结果是按照升序或降序排列。默认情况下，它是按照升序排列的。

你可以添加WHERE...LIKE子句来设置条件

> 分组

GROUP BY语句根据一个或者多个列对结果集进行分组。在分组的列上我们可以使用COUNT,SUM,ACG 等函数。

语法 ：

```bash
SELECT column_name , function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
```

### other

> 获取表中字段名

`SHOW CREATE TABLE table_name`

> 在表中添加字段

`ALTER TABLE table_name ADD column_name VARCHAR(20)`



