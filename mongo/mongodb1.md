# mongoDB CRUD

tags:mongodb

## create database
使用`use [database_name]`来创建数据库，如果数据库不存在则创建数据库，如果存在就切换到数据库。

```
use blackhole
```
## delete database
`db.dropDatabase()`
删除当前的数据库
## insert data
- insertOne()  (3.2 new)
- insertMany()   (3.2 new)
- insert()
`db.COLLECTION_NAME.insert(document)`

```
>db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})

db.users.insertMany(
   [
      { name: "sue", age: 26, status: "pending" },
      { name: "bob", age: 25, status: "enrolled" },
      { name: "ann", age: 28, status: "enrolled" }
   ]
)
```
col（集合，如果不存在会自动创建该集合）

## update data
###1 update
```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```
参数说明：

- query : update的查询条件，类似sql update查询内where后面的。
- update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
- upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
- multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
- writeConcern :可选，抛出异常的级别。
- 
```
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })   # 输出信息
> db.col.find().pretty()
{
        "_id" : ObjectId("56064f89ade2f21f36b03136"),
        "title" : "MongoDB",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
>
```
### 2 save()
save() 方法通过传入的文档来替换已有文档。语法格式如下：

```
db.collection.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

参数说明：

- document : 文档数据。
- writeConcern :可选，抛出异常的级别。


```
>db.col.save({
	"_id" : ObjectId("56064f89ade2f21f36b03136"),
    "title" : "MongoDB",
    "description" : "MongoDB 是一个 Nosql 数据库",
    "by" : "Runoob",
    "url" : "http://www.runoob.com",
    "tags" : [
            "mongodb",
            "NoSQL"
    ],
    "likes" : 110
})
```

## 查询query
### find
`db.collection.find()`
 可以与`limits` `skips` `sort` `orders`一起使用

```
查询 大于18 名字是jack 只返回 name 地址
db.users.find({age:{$gt:18},name:"jack"},{name:1,address:1}).limit(5)

//or 查询
db.users.find({
    $or:[{age:{$gt:18}},{name:"jack"}]},{name:1,address:1}).limit(5)

db.users.find({age:{$gt:18},name:"jack"},{name:1,address:1}).limit(5)
db.users.find({age:{$gt:18}},{name:1,address:1}).limit(5)

db.user.find({"age":{$lt:18}}).sort({age:1})

这查询从 user 集合中选择符合条件 age 大于 18 的文档。为了指定大于条件，
查询条件使用大于（也就是 $gt ） query selection operator 。
这个查询最多返回 5 个匹配的文档（或者更准确的说，一个指向这些文档的游标）。
这些匹配的文档将仅仅返回 _id， name 和 address 字段。详细信息，请参阅 映射 。

## 返回指定的字段
db.user.find({},{name:1})
## select name from user;

##排除字段
db.user.find({},{sex:0,name:0})

## 嵌套查询
db.match.find({idNum:"610404199604151013"},{"jsonparams.name":1,matchId:1})
```

- `$lt`(<),`$gt`(>),`$gte`(>=),`$lte`(<=),`$eq`(<=),`$ne`(!=)
- 
```
db.user.find({"age":{$lt:18}}).sort({age:1})
```
- `$in` 
- 
```
db.user.find({"age":{$in:[12,14]}}).sort({age:1})
```
- `nin` `{ field: { $nin: [ <value1>, <value2> ... <valueN> ]} }`
    - 字段不在值中
    - 字段不存在的记录
    
```
db.user.find({"asd":{$nin:["add"]}})
```
- `$not` : `{ field: { $not: { <operator-expression> } } }`

- `$exists` : `{ field: { $exists: <boolean> } }`
当<boolean>的值为true的时候查询出所有包含field字段的记录
当<boolean>的值为false的时候查询出所有不包含field字段的记录

```
db.user.find({"asdd":{$exists:false}})
```
### Cursors


## delete document
remove()

```
db.collection.remove(<query,<justOne>)
```
2.6 之后的语法

```
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```

参数说明：

- query :（可选）删除的文档的条件。
- justOne : （可选）如果设为 true 或 1，则只删除一个文档。
- writeConcern :（可选）抛出异常的级别。


```
// 数组里面增加元素 push会重复的插入数据（导致重复数据）
db.t_match_teamapply.update({"teamId":"A0012"},{$push:{"membsers":ObjectId("56cac6bb83d407efc0d04eaa")}})
db.t_match_teamapply.update({"teamId":"A0012"},{$push:{"membsers":ObjectId("56cac6bb83d407efc0d04eac")}})
//$ne 用来判断数据是否存在，存在就不插入

db.t_match_teamapply.update({"membsers":{$ne:ObjectId("56cac5bc83d407efc0d04ea9")}},{$push:{"membsers":ObjectId("56cac5bc83d407efc0d04ea9")}})
//$addToSet比$ne更好用，它可以自己判断数据是否存在，而且它和$each结合使用，还能同时在数组中插入多个数据

db.t_match_teamapply.update({"teamId":"A0012"},{$addToSet:{"membsers":{$each:[ObjectId("56cac6bb83d407efc0d04eaa"),ObjectId("56cac6bb83d407efc0d04eac")]}}})                    



// 更新
db.t_match_teamapply.update({"_id":ObjectId("56cac5bc83d407efc0d04ea9")},{$set:{"teamId":"A0013"}})
// 删除数组里面的元素
db.t_match_teamapply.update({"teamId":"A0012"},{$pop:{"membsers":1}}) // 后面删除1
db.t_match_teamapply.update({"teamId":"A0013"},{$pop:{"membsers":1}}) //前面删除1

//删除中间的数据(其实可以是任意的位置)
db.t_match_teamapply.update({"teamId":"A0013"},{$pull:{"membsers":ObjectId("56cac5bc83d407efc0d04ea9"}}) 



```


