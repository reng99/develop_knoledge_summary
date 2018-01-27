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

有待补充












