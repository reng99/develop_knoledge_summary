## 基本操作

> 创建并查看数据库

 创建 ： `$ use database_name`
 
 查看 ： `$ show dbs`
 
 ⚠️ 在创建一个空数据库之后进行查看，是不会显示已经创建的数据库的，你需要往数据库里面添加一些数据才行。
 
 `$ db.database_name.insert({"key":"value"})`，这时候使用`$ show dbs`才会显示你创建的数据库。
