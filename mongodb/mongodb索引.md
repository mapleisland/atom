mongodb索引的种类:
- **\_id** 索引 - 是绝大多数集合默认建立的索引
- **单键** 索引 - 是最普通的索引,不会自动创建
- **多键** 索引 -
- **复合** 索引 -
- **过期** 索引 - 在一段时间后会过期的索引,过期后相应的数据会被删除  
储存在过期索引字段的值必须是指定的时间类型(ISODate或者ISODate数组,不能使用时间戳,否则不能被自动删除)
- **全文** 索引 -
- **地理位置** 索引 -

索引格式
```
//创建索引的一般格式,第一个参数是索引的值,第二个是索引的属性
> db.collectionName.ensureIndex({param},{param});
```
比较重要的索引属性有:
- 索引名字
```
> db.collectionName.ensureIndex({},{name:"indexName"});
```
- 唯一性,即插入的数据不能重复
```
> db.collectionName.ensureIndex({},{unique:true/false});
```
- 稀疏性
```
> db.collectionName.ensureIndex({},{sparse:true/false});
```
- 是否定时删除
```
> db.collectionName.ensureIndex({},{expireAfterSeconds:60});
```
---
```
//查询索引
> db.collectionName.getIndexes();
[
  {
    "v" : 1,
    "key" : {
      "_id" : 1
    },
    "name" : "_id_",
    "ns" : "dbName.collectionName"
  },
  {
    "v" : 1,
    "key" : {
      "x" : 1
    },
    "name" : "x_1",
    "ns" : "dbName.collectionName"
  }
]
```
查询索引返回值中name属性为索引的名字,如果不在创建时指定,系统会自动命名

---
```
//创建单键索引
> db.collectionName.ensureIndex({x:1});

//创建多键索引
> db.collectionName.ensureIndex({x:[1,2,3,4,5]});

//创建复合索引
> db.collectionName.ensureIndex({x:1,y:1});

//创建全文索引
> db.collectionName.ensureIndex({x:"text"});

//查找全文索引1,查找包含keyword1的内容
> db.collectionName.find({$text:{$search:"kw1"}})

//查找全文索引2,空格间是或逻辑,包含kw1或kw2或kw3都会被命中
>db.collectionName.find({$text:{$search:"kw1 kw2 kw3"}})

//查找全文索引3,查找包含kw1或kw2且不包含kw3的内容
> db.collectionName.find({$text:{$search:"kw1 kw2 -kw3"}})

//查找全文索引2,将关键字用引号包起来形成与逻辑,包含kw1且kw2且kw3都会被命中
> db.collectionName.find({$text:{$search:"\"kw1\" \"kw2\" \"kw3\""}})

//删除索引
> db.collectionName.dropIndex("indexName");
```
