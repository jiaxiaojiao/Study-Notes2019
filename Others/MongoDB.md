# MongoDB

## 为什么我们要使用MongoDB？
特点:
- 高性能、易部署、易使用，存储数据非常方便。主要功能特性有：
- 面向集合存储，易存储对象类型的数据。
- 模式自由。
- 支持动态查询。
- 支持完全索引，包含内部对象。
- 支持查询。
- 支持复制和故障恢复。
- 使用高效的二进制数据存储，包括大型对象（如视频等）。
- 自动处理碎片，以支持云计算层次的扩展性
- 支持Python，PHP，Ruby，Java，C，C#，Javascript，Perl及C++语言的驱动程序，社区中也提供了对Erlang及.NET等平台的驱动程序。
- 文件存储格式为BSON（一种JSON的扩展）。
- 可通过网络访问。

功能:
- **面向集合的存储**：适合存储对象及JSON形式的数据。
- **动态查询**：Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
- **完整的索引支持**：包括文档内嵌对象及数组。Mongo的查询优化器会分析查询表达式，并生成一个高效的查询计划。
- **查询监视**：Mongo包含一个监视工具用于分析数据库操作的性能。
- **复制及自动故障转移**：Mongo数据库支持服务器之间的数据复制，支持主-从模式及服务器之间的相互复制。复制的主要目标是提供冗余及自动故障转移。
- **高效的传统存储方式**：支持二进制数据及大型对象（如照片或图片）
- **自动分片以支持云级别的伸缩性**：自动分片功能支持水平的数据库集群，可动态添加额外的机器。

适用场合:
- 网站数据：Mongo非常适合实时的插入，更新与查询，并具备网站实时数据存储所需的复制及高度伸缩性。
- 缓存：由于性能很高，Mongo也适合作为信息基础设施的缓存层。在系统重启之后，由Mongo搭建的持久化缓存层可以避免下层的数据源 过载。
- 大尺寸，低价值的数据：使用传统的关系型数据库存储一些数据时可能会比较昂贵，在此之前，很多时候程序员往往会选择传统的文件进行存储。
- 高伸缩性的场景：Mongo非常适合由数十或数百台服务器组成的数据库。Mongo的路线图中已经包含对MapReduce引擎的内置支持。
- 用于对象及JSON数据的存储：Mongo的BSON数据格式非常适合文档化格式的存储及查询。

需要注意的问题：
1. 因为MongoDB是全索引的，所以它直接把索引放在内存中，因此最多支持2.5G的数据。如果是64位的会更多。
2. 因为没有恢复机制，因此要做好数据备份
3. 因为默认监听地址是127.0.0.1，因此要进行身份验证，否则不够安全；如果是自己使用，建议配置成localhost主机名
4. 通过GetLastError确保变更

## MongoDB结构介绍

MongoDB中存储的对象时BSON，是一种类似JSON的二进制文件，它是由许多的键值对组成。如下所示： 
```text
{  "name" : "huangz",  "age" : 20,  "sex" : "male"  }  {    "name" : "jack",  "class" : 3,   "grade" : 3  }
```
而数据库的整体结构组成如下：
```text
键值对 => 文档 => 集合 => 数据库
```

MongoDB的文件单个大小不超过4M，但是新版本后可提升到16M。

## MongoDB中的key命名规则
- "\0"不能使用
- 带有"."号，"_"号和"$"号前缀的Key被保留
- 大小写有区别，Age不同于age
- 同一个文档不能有相同的Key
- 除了上面几条规则外，其他所有UTF-8字符都可以使用

## 常用命令
```text
1 #进入数据库

use admin

2 #增加或修改密码

db.addUser('xingoo','123')

db.addUser("xingoo","123",true) 参数分别为 用户名、密码、是否只读

3 #查看用户列表

db.system.users.find()

4 #用户认证

db.auth('xingoo','123')

5 #删除用户

db.removeUser('xingoo')

6 #查看所有用户

show users

7 #查看所有数据库

show dbs

8 #查看所有的collection集合

show collections

9 #查看各个collection的状态

db.printCollectionStats()

10 #查看主从复制状态

db.printReplicationInfo()

11 #修复数据库

db.repairDatabase()

12 #设置profiling,0:off 1:slow 2 all

db.setProfilingLevel(1)

13 #查看profiling

show profiling

14 #拷贝数据库

db.copyDatabase('xingootest','xingootest1')

db.copyDatabase("xingootest","temp","127.0.0.1")

15 #删除集合collection

db.xingootest.drop()

16 #删除当前数据库

db.dropDatabase()
```

## MongoDB增删改命令

```text
1 #存储嵌套的对象

db.foo.save({'name':xingoo,'age':25,'address':{'city':'changchun','Province':'Jilin'}})

2 #存储数组对象

db.foo.save({'name':xingoo,'age':25,'address':['Jilin Province','Liaoning Province']})

3 #根据query条件修改，如果不存在则插入，允许修改多条记录

db.foo.update({'age':'25'},{'$set':{'name':'xingoo'}},upsert=true,multi=true)

4 #删除yy=5的记录

db.foo.remove({'name':'xingoo'})

5 #删除所有的记录

db.foo.remove()
```

## 索引
```text
1 #增加索引:1 asc -1 desc

db.foo.ensureIndex({firstname:1,lastname:-1},{unieap:true})

2 #索引子对象(不懂)

db.foo.ensureIndex({'Al.Em':!})

3 #查看索引信息

db.foo.getIndexes()

db.foo.getIndexKeys()

4 #根据索引名删除索引(不懂)

db.foo.dropIndex('Al.Em_1')

```

## 查询
```text
条件操作符

 1$gt ---- > 2 $lt ---- < 3$gte ---- >= 4 $lte ---- <= 5$ne ---- != 、<> 6$in ---- in 7$nin ---- not in 8$all ---- all 9$or ---- or10$not ---- 反匹配

1 #查询所有记录

db.foo.find() ---- select * from foo

2 #查询某列非重复的记录

db.foo.distinct("xingoo") ---- select distinct name from foo

3 #查询age = 22 的记录

db.foo.find({"age":22}) ---- select * from foo where age = 22

4 #查询age > 22 的记录

db.foo.find({age:{$gt:22}}) ---- select * from foo where age > 22

5 #查询age < 22 的记录

db.foo.find({age:{$lt:22}}) ---- select * from foo where age < 22

6 #查询age <= 25的记录

db.foo.find({age:{$lte:25}})

7 #查询age >= 23 并且 age <=26的记录

db.foo.find({age:{lte:26}})

8 #查询name中包含xingoo的数据

db.foo.find({name:/xingoo/}) ---- select * from foo where name like '%xingoo%'

9 #查询name中以xingoo开头的数据

db.foo.find({name:/^xingoo/}) ---- select * from foo where name like 'xingoo%'

10 #查询指定列name、age的数据

db.foo.find({},{name:1,age:1}) ---- select name,age from foo

11 #查询制定列name、age数据，并且age > 22

db.foo.find({age:{$gt:22}},{name:1,age:1}) ---- select name,age from foo where age >22

12 #按照年龄排序

升序：db.foo.find().sort({age:1})  降序：db.foo.find().sort({age:-1})

13 #查询name=xingoo.age=25的数据

db.foo.find({name:'xingoo',age:22}) ---- select * from foo where name='xingoo' and age ='25'

14#查询前5条数据

db.foo.find().limit(5) ---- select top 5 * from foo

15 #查询10条以后的数据

db.foo.find().skip(10) ---- select * from foo where id not in (select top 10 * from foo);

16 #查询在5-10之间的数据

db.foo.find().limit(10).skip(5) 

17 #or与查询

db.foo.find({$or:[{age:22},{age:25}]}) ---- select * from foo where age=22 or age =25

18 #查询第一条数据

db.foo.findOne() 、db.foo.find().limit(1)---- select top 1 * from foo

19 #查询某个结果集的记录条数

db.foo.find({age:{$gte:25}}).count() ---- select count(*) from foo where age >= 20

20 #按照某列进行排序(不懂)

db.foo.find({sex:{$exists:true}}).count() ---- select count(sex) from foo

21 #查询age取模10等于0的数据

db.foo.find('this.age % 10 == 0')、db.foo.find({age:{$mod:[10,0]}})

22 #匹配所有

db.foo.find({age:{$all:[22,25]}})

23 #查询不匹配name=X*带头的记录

db.foo.find({name:{$not:/^X.*/}})

24 #排除返回age字段

db.foo.find({name:'xingoo'},{age:0})

25 #判断字段是否存在

db.foo.find({name:{$exists:true}})

管理

1 #查看collection数据大小

db.xingootest.dataSize()

2 #查看collection状态

db.xingootest.stats()

3 #查询所有索引的大小

db.xingootest.totalIndexSize()

参考资料：

【MongoDB介绍及安装】http://database.51cto.com/art/201103/247882.htm

【MongoDB使用入门】http://www.linuxidc.com/Linux/2013-01/78251.htm
```