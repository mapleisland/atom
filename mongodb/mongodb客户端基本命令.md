mongodb的基本概念:  
数据库,集合,文档,域
```
//显示所有数据库
> show dbs

//切换数据库
> use dbname

//插入数据
> db.dbname.insert({jsondata:"jsondata"})

//查询所有数据
> db.dbname.find()

//查询特定数据
> db.dbname.find({data:"data i want to find"})

//查询数据条数
> db.dbname.find().count()

//跳过前几条数据
> db.dbname.find().skip(3)

//只取得n条数据
> db.dbname.find().limit(3)

//按field排序
> db.dbname.find().sort({x:1})

//更新文档,完整更新,文档内容会变为之后设置的json数据
> db.dbname.update({x:1},{x:99})

//更新文档,部分更新,设定的内容会更新
> db.dbname.update({x:1},{$set:{x:99}})
```
