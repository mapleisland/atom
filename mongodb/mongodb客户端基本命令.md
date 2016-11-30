mongodb相比sql数据库的基本概念:
```
/--------------------------------------------------\
| SQL            | MongoDB        | comment        |
| -------------- | -------------- | -------------- |
| database       | database       | 数据库          |
| table          | collection     | 数据表/集合     |
| row            | document       | 数据记录行/文档 |
| column         | field          | 数据字段/域     |
| index          | index          | 索引            |
| table joins    |                | 表联合          |
| primary key    | primary key    | 主键            |
\--------------------------------------------------/
```
mongodb基本命令(增删改查):
```
//显示所有数据库
> show dbs

//切换数据库
> use dbName

//插入数据
> db.collectionName.insert({jsondata:"jsondata"})

//查询所有数据
> db.collectionName.find()

//查询特定数据
> db.collectionName.find({x:1})

//查询数据条数
> db.collectionName.find().count()

//跳过前几条数据
> db.collectionName.find().skip(3)

//只取得n条数据
> db.collectionName.find().limit(3)

//按field排序
> db.collectionName.find().sort({x:1})

//更新文档,完整更新,文档内容会变为之后设置的json数据
> db.collectionName.update({x:1},{x:2})

//更新文档,部分更新,设定的内容会更新
> db.collectionName.update({x:1},{$set:{x:2}})

//更新时如果查询条件不存在则自动创建
> db.collectionName.update({x:1},{x:2},true)

//更新所有匹配项目,查找到所有的{x:1}的文档并且更新
> db.collectionName.update({x:1},{$set:{x:2}},false,true)

//删除数据
> db.collectionName.remove({x:1})

//删除表
> db.collectionName.drop()
```
