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

> mongodb 关系

mongodb的关系表示多个文档之间在逻辑上的相互联系。

文档间可以通过嵌入和引用来建立关系。

mongodb中的关系可以是：

1:1（一对一）

1:n（一对多）

n:1（多对一）

n:n（多对多）

下面例子demo考虑用户与用户地址的关系：一个用户可以有多个地址，所以是一对多的关系。

以下是user文档的简单结构：

```bash
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "name": "Tom Hanks",
   "contact": "987654321",
   "dob": "01-01-1991"
}
```

以下是address文档的简单结构：

```bash
{
   "_id":ObjectId("52ffc4a5d85242602e000000"),
   "building": "22 A, Indiana Apt",
   "pincode": 123456,
   "city": "Los Angeles",
   "state": "California"
} 
```

**嵌入式关系**

使用嵌入式方法，我们可以将用户地址嵌入到用户的文档中：

```bash
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin",
   "address": [
      {
         "building": "22 A, Indiana Apt",
         "pincode": 123456,
         "city": "Los Angeles",
         "state": "California"
      },
      {
         "building": "170 A, Acropolis Apt",
         "pincode": 456789,
         "city": "Chicago",
         "state": "Illinois"
      }]
} 
```

以上数据保存在单一的文档中，可以比较容易的获取和维护数据。你可以这样查询用户的地址：

```bash
> db.users.findOne({"name":"Tom Benzamin"},{"address":1})
```

但是这种嵌套的结构的缺点是，如果用户和地址在不断的增加，数据量不断变大，会影响读写性能。

**引用式关系**

引入式关系是设计设计数据库时经常用到的方法，这种方法把用户数据文档和用户地址数据文档分开，通过引用文档的id字段来建立关系。

```bash
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin",
   "address_ids": [
      ObjectId("52ffc4a5d85242602e000000"),
      ObjectId("52ffc4a5d85242602e000001")
   ]
}
```

以上实例中，用户文档的address_ids字段包含用户地址的对象id数组。

我们可以读取这些用户地址的对象id来获取用户的详细地址信息。

这种方法需要两次的查询，第一次查询用户地址对应的对象id，第二次通过查询的id获取用户的详细地址信息。

```bash
> var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1});
> var addresses = db.address.find("_id":{"$in":result["address_ids"]});
```

> 数据库引用

mongodb数据库引用的方式有两种：一种是`手动引用（manual references）`另一种是`dbrefs`。

**dbrefs vs 手动引用**

考虑这样的一个场景，我们在不同的集合中（address_home,address_office,address_mailing,等）存储不同的地址（住址，办公室地址，邮件地址等）。

这样，我们在调用不同地址时，也需要指定集合，一个文档从多个集合引用文档，我们应该使用dbrefs。

**使用数据库引用（dbrefs）**

数据库引用的形式：

`{$ref:,$id:,$db:}`

三个字段表示的意思：

$ref： 集合名称

$id： 引用的id

$db： 数据库名称（可选参数）

demo如下所示：

实例中用户数据是使用了dbref，字段address:

```bash
{
   "_id":ObjectId("53402597d852426020000002"),
   "address": {
   "$ref": "address_home",
   "$id": ObjectId("534009e4d852427820000002"),
   "$db": "runoob"},
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin"
}
```

address DBRef 字段指定了引用的地址文档是在 address_home 集合下的 runoob 数据库，id 为 534009e4d852427820000002。

以下代码中，通过指定$ref参数（address_home集合）来查找集合中指定的id的用户地址信息：

```bash
> var user = db.users.findOne({"name":"Tom Benzamin"})
> var dbRef = user.address
> db[dbRef.$ref].findOne({"_id":(dbRef.$id)})
```

 然后就返回了address_home集合中的地址数据：
 
 ```bash
 {
   "_id" : ObjectId("534009e4d852427820000002"),
   "building" : "22 A, Indiana Apt",
   "pincode" : 123456,
   "city" : "Los Angeles",
   "state" : "California"
}
 ```
 
> 原子操作

mongodb不支持事务，所以，在项目中应用时，要注意这点。无论什么设计，都不要要求mongodb保证数据的完整性。但是mongodb提供了许多原子操作，比如文档的保存，修改和删除等，都是原子操作。

所谓原子操作就是要么保存这个文档到mongodb，要么没有保存到mongodb，不会出现查询到的文档没有保存完整的情况。

**原子操作数据模型**

考虑下面的demo，图书馆的书籍及结账信息。

实例说明了在一个相同的文档是如何嵌入字段关联原子操作（update:更新）的字段是同步的。

```bash
book = {
          _id: 123456789,
          title: "MongoDB: The Definitive Guide",
          author: [ "Kristina Chodorow", "Mike Dirolf" ],
          published_date: ISODate("2010-09-24"),
          pages: 216,
          language: "English",
          publisher_id: "oreilly",
          available: 3,
          checkout: [ { by: "joe", date: ISODate("2012-10-15") } ]
        }
```

你可以使用db.collection_name.findAndModify()方法来判断书籍是否可结算并更新新的结算信息。

在同一个文档中嵌入的available和checkout字段来确保这些字段是同步更新的。

```bash
db.books.findAndModify ( {
   query: {
            _id: 123456789,
            available: { $gt: 0 }
          },
   update: {
             $inc: { available: -1 },
             $push: { checkout: { by: "abc", date: new Date() } }
           }
} )
```

**原子操作常用的命令**

$set -> 用来指定一个键并更新键值，若键不存在并创建。`{$set:{field: value}}`。

$unset -> 用来删除一个键。 `{ $unset : { field : 1 } }`。

$inc -> 可以对文档的某个值为数字型（只能为满足要求的数字）的键进行增减的操作。`{ $inc : { field : value }}`。

$push ->  把value追加到field里面去，field一定要是数组类型才行，如果field不存在，会增加一个数组类型加进去。

$pushAll -> 同$push，只是一次可以追加多个值到一个数组字段内。`{ $pushAll : { field : value_array }}`。

$pull -> 从数组field内删除一个等于value值。`{ $pull : { field : _value } }`。

$addToset -> 增加一个值到数组内，而且只有当这个值不在数组内才增加。 `{ $addToSet : { field : _value }}`。

$pop -> 删除数组的第一个或最后一个元素。`{ $pop : { field : 1 }}`。

$rename -> 修改字段名称。 `{ $rename : { old_field_name : new_field_name }}`

$bit -> 位操作，integer类型。 `{ $bit : { field : {and : 5} } }`

偏移操作符 -> 

```bash
> t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 3 }, { "by" : "jane", "votes" : 7 } ] }
 
> t.update( {'comments.by':'joe'}, {$inc:{'comments.$.votes':1}}, false, true )
 
> t.find() { "_id" : ObjectId("4b97e62bf1d8c7152c9ccb74"), "title" : "ABC", "comments" : [ { "by" : "joe", "votes" : 4 }, { "by" : "jane", "votes" : 7 } ] }
```

> 高级索引

考虑以下文档集合（users）：

```bash
{
   "address": {
      "city": "Los Angeles",
      "state": "California",
      "pincode": "123"
   },
   "tags": [
      "music",
      "cricket",
      "blogs"
   ],
   "name": "Tom Benzamin"
}
```

以上的文档包含了address子文档和tags数组。

**索引数组字段**

假设我们基于标签来检索用户，为此我们需要对集合中的数组tags建立索引。

在数组中创建索引，需要我们对数组中的每个字段依次建立索引。所以在我们为数组tags创建索引时，会为music,cricket,blogs三个值建立单独的索引。

使用以下命令创建数组索引：

```bash
> db.users.ensureIndex({"tags":1}
```

创建索引后，我们可以这样检索集合的tags字段：

```bash
> db.users.find({tags : "cricket"})
```

为了验证我们使用了索引，我们可以使用explain命令：

 ```bash
 > dn.user.find({tags:"cricket"}).explain()
 ```
 
 以上的命令执行的结果中会显示"cursor":"BtreeCursor tags_1"，则表示已经使用了索引。
 
 **索引子文档字段**
 
 假设我们需要通过city,state,pincode字段来检索文档，由于这些字段是子文档的字段，所以我们需要对子文档建立索引。
 
 为子文档的三个字段创建索引，命令如下：
 
 ```bash
 > db.users.ensureIndex({"address.city":1,"address.state":1,"address.pincode":1})
 ```
 
 一旦创建索引，我们就可以使用子文档的字段来检索数据：
 
 ```bash
 > db.users.find({"address.city":"Los Angeles"})
 ```
 
 记住查询表达式必须遵循指定的索引的顺序。所以上面创建的索引将支持以下查询：
 
 ```bash
 db.users.find({"address.city":"Los Angeles","address.state":"California"})
 ```
 
 同样支持以下查询：
 
 ```bash
 > db.users.find({"address.city":"Los Angeles","address.state":"California","address.pincode":"123"})
 ```
 
> 索引限制

**额外开销**

每个索引占据一定的存储空间，在进行插入，更新和删除操作时也需要对索引进行操作。所以，如果你很少对集合进行读取操作，建议不使用索引。

**内存（ram）使用**

由于索引是存储在内存（ram）中，你应该确保改索引的大小不超过内存的限制。

如果索引的大小大于内存的限制，mongodb会产出一些索引，这将导致性能下降。

**查询限制**

索引不能被以下的查询使用：

- 正则表达式及非操作符，如$nin,$not，等。

- 算数运算符，如$mod,等

- $where子句

所以，检测你的语句是否使用索引是一个好习惯，可以用explain来查看。

**索引键限制**

从2.6版本开始，如果现有的索引字段超过索引键的限制，mongodb中不会创建索引。

**插入文档超过索引键限制**

如果文档的索引字段超过了索引键限制，mongodb不会将任何文档转换成索引的集合。与mongorestore和mongoimport工具类似。

**最大范围**

- 集合中索引不能超过64个

- 索引名的长度不能超过128字符

- 一个复合索引最多可以有32个字段

> ObjectId

ObjectId是一个12字BSON类型的数据，有以下格式：

- 前4个字节表示时间戳

- 接下来的3个字节就是机器标识码

- 紧接的两个字节由进程id组成（pid）

- 最后三个字节是随机数

mongodb中存储的文档必须由一个*_id键。这个键的值可以是任何类型的，默认是个ObjectId对象。

在一个集合里面，每个文档都有唯一的*_id值，来确保集合里面每个文档都能被唯一标识。

mongodb采用了ObjectId，而不是其他比较常规的做法（比如自动增加的主键）的主要原因，因为在多个服务器上同步自动增加主键值既费力还费时。

**创建新的ObjectId**

使用以下的代码生成新的objectid:

```bash
> newObjectId = ObjectId()
```
上面的语句会返回唯一生成的id,你也可以使用生成的id来取代mongodb自动生成的objectid:

```bash
> myObjectId = ObjectId("your id number here")
```

**创建文档的时间戳**

由于objectid中存储了四个字节的时间戳，所以你不需要为你的文档保存时间戳字段，你可以通过getTimestamp函数来获取文档的创建时间。

```bash
> ObjectId("5349b4ddd2781d08c09890f4").getTimestamp()
```

上面的代码将返回iso格式的文档创建时间：

```bash
ISODate("2014-04-12T21:49:17Z")
```

**ObjectId转换为字符串**

在某些情况下，你可能需要将objectid转换为字符串格式。你可以使用`> new ObjectId().str`

> map reduce

map reduce是一种计算模型，简单的说就是将大批量的工作（数据）分解（map）执行，然后再将结果合并成最终结果（reduce）。

mongodb提供的map-reduce非常灵活，对于大规模数据分析也相当实用。

**mapreduce命令**

以下是mapreduce的基本用法：

```bash
> db.collection.mapReduce(
 function() {emit(key,value);}, // map函数
 function(key,value) {}
)
```

## 注意

注意⚠️  本文件的学习点参考自http://www.runoob.com/mongodb/mongodb-tutorial.html



