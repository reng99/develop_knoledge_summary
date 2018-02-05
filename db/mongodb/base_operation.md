## 基本操作

建议每个命令行后面都添加一个分号`;`，这样就可以避免不时的报语法错误啦。

> 创建并查看数据库

 创建 ： `> use database_name;`
 
 查看 ： `> show dbs;`
 
 ⚠️ 在创建一个空数据库之后进行查看，是不会显示已经创建的数据库的，你需要往数据库里面添加一些数据才行。
 
 `> db.database_name.insert({"key":"value"});`，这相当你自己已经创建了一个名为`reng`的集合了，这时候使用`$ show dbs`才会显示你创建的数据库。
 
 或者直接创建集合并插入数据才行。
 
 ```bash
 > use database_name;
 > db.createCollection("table_name",option_obj);
 > db.table_name.insert(option);
 > show dbs;
 ```
 
 > 删除数据库
 
 `> db.dropDatabase();`
 
 进入需要删除的数据库，然后执行上面的命令行。
 
 ```bash
 > use database_name;
 > db.dropDatabase();
 ```
 
>  创建集合

`> db.createCollection(name,options)`

需要进入相关的数据库,然后才能创建集合（表）。

demo:
```bash
> use reng;
> db.createCollection("jia",{name : true});
> db.jia.insert({"name":"jiaming"});
> show tables;
jia
```

> 删除集合

`> db.collection_name.drop()`

进入相关的数据库，删除存在的集合,以上面新建好的集合`jia`为例子：

```bash
> use reng;
> show tables;
jia
> db.jia.drop();
true
> show tables;

```

> 插入文档

`db.collection_name.insert(document)`

demo:

```bash
db.collection_name({
 title: "this is the title"
})；
```

> 更新文档

使用`update()`方法更新已经存在的文档。语法格式如下：

```bash
db.collection_name.update(
 <query>,
 <update>,
 {
   upsert: <boolean>,
   multi: <boolean>,
   writeConcern: <document>
 }
)
```

参数说明 ：

query: update的查询条件，类似sql update查询内where后面的条件。

update: update的对象和一些更新的操作符（如$.$inc...）等，也可以理解为sql update查询内set后面的内容。

upsert: 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false,不插入。

multi: 可选，mongodb默认是false，只更新找到的第一条记录，如果这个参数为true,就是把按条件查出来多条记录全部更新。

writeConcern: 可选，抛出异常的级别。

> 删除文档

使用`remove()`版本2.6后的语法：

```bash
db.collection_name.remove(
 <query>,
 {
  justOne: <boolean>,
  writeConcern: <boolean>
 }
)
```

参数说明：

query: 可选，删除的文档条件。

justOne: 可选，如果设置为true或1，则只删除一个文档。

writeConcern: 可选，抛出异常的级别。

> 查询文档

通过`find()`方法以非结构化的方式来显示所有文档。

语发 ：

`db_collection_name.find(query,projection)`

参数说明：

query : 可选，使用查询操作符指定查询条件。

projection : 可选，使用投影操作符指定返回的键。查询时返回文档中所有键值，只需要省略该参数就可以了（默认省略）。

如果你需要以易读的方式读取数据，可以使用`pretty()`方法，语法格式如下：

```bash
> db.collection_name.find().pretty()
```

> limit和skip方法

使用`limit()`方法读取指定数量的数据记录；语法如下：

```bash
> db.collection_name.find().limit(NUMBER)
```

可以使用`skip()`方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。

```bash
> db.collection_name.find().limit(NUMBER).skip(NUMBER);
```

> 排序

使用`sort()`方法对数据进行排序，`sort()`方法可以通过参数指定排序的字段，并使用1和-1来指定排序的方式，其中1为升序排序，而-1是用于降序排列。基本语法如下：

```bash
> db.collection_name.find().sort({KEY:1});
```

> ⚠️ 索引

索引通常能够极大的提高查询的效率，如果没有索引，mongodb在读取数据时候必须扫描集合中的每个文件并选取那些符合查询条件的记录。

这种扫描全集合的查询效率是非常低的，特别是在处理大量的数据时，查询可能要花费几十秒甚至几分钟，这对网站的性能是非常致命的。

索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或者多列的值进行排序的一种结构。

使用`ensureIndex()`方法来创建索引。

```bash
> db.collection_name.ensureIndex({key:1}) // key值为你要创建的索引字段，1为指定按照升序创建索引
```

> 聚合

mongodb中的聚合（aggregate）主要是用于处理数据（诸如统计平均值，求和等），并返回计算后的数据结果。有点类似mysql中的count(*)。

aggregate的语法：

```bash
> db.collection_name.aggregate(AGGREGATE_OPERATION)
```

这个难清楚，还是来个demo比较好：

```bash
{
   _id: ObjectId(7df78ad8902c)
   title: 'MongoDB Overview', 
   description: 'MongoDB is no sql database',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 100
},
{
   _id: ObjectId(7df78ad8902d)
   title: 'NoSQL Overview', 
   description: 'No sql database is very fast',
   by_user: 'runoob.com',
   url: 'http://www.runoob.com',
   tags: ['mongodb', 'database', 'NoSQL'],
   likes: 10
},
{
   _id: ObjectId(7df78ad8902e)
   title: 'Neo4j Overview', 
   description: 'Neo4j is no sql database',
   by_user: 'Neo4j',
   url: 'http://www.neo4j.com',
   tags: ['neo4j', 'database', 'NoSQL'],
   likes: 750
},
```
```bash
> db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
{
   "result" : [
      {
         "_id" : "runoob.com",
         "num_tutorial" : 2
      },
      {
         "_id" : "Neo4j",
         "num_tutorial" : 1
      }
   ],
   "ok" : 1
}
>
```



