# MongoDB
## 什么是MongoDB
是用c++编写的，基于分布式分拣存储的开源数据库系统。

SQL术语/概念 | MongoDB术语/概念| 解释/说明
--------- | -------------|-----
database  | database|数据库
table  | collection|数据库表/集合
row  | document|数据记录行、文档
column  | field|数据字段、域
index  | index|索引
table joins  |  |表连接，mongo不支持
primary key|primary key| 主键、mongodb自动将_id 设置为主键

![](media/14537043531094/14537050269370.jpg)


## start mongodb

```
./mongod -config ../../mongodata/mongod.conf
```

##stop mongodb

```
//1、方式一
use admin
db.shutdownServer()
//2
mongod --shutdown

```

## 使用
### 登陆
```
./mongo 	#login on mongo client

# show all the dbs
> show dbs
local   0.078GB
test    0.078GB
testdb  0.078GB

#show current database
> db
test

#change database
> use testdb
switched to db testdb

```

##文档
文档是一个键值(key-value)对(即BSON)。MongoDB 的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，这与关系型数据库有很大的区别，也是 MongoDB 非常突出的特点。

```
{"site":"www.runoob.com", "name":"菜鸟教程"}
```
## collection
集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性。

```
{"site":"www.baidu.com"}
{"site":"www.google.com","name":"Google"}
{"site":"www.runoob.com","name":"菜鸟教程","num":5}
```
当第一个文档插入时，集合就会被创建。
合法的集合名
集合名不能是空字符串""。
集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
集合名不能以"system."开头，这是为系统集合保留的前缀。
用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。　

MongoDB 数据类型
下表为MongoDB中常用的几种数据类型。

数据类型	| 描述
-------|-----
String	|字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 |编码的字符串才是合法的。
Integer	|整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。
Boolean	|布尔值。用于存储布尔值（真/假）。
Double	|双精度浮点值。用于存储浮点值。
Min/Max keys	|将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。
Arrays	|用于将数组或列表或多个值存储为一个键。
Timestamp	|时间戳。记录文档修改或添加的具体时间。
Object	|用于内嵌文档。
Null	|用于创建空值。
Symbol	|符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。
Date	|日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。
Object ID	|对象 ID。用于创建文档的 ID。
Binary Data	|二进制数据。用于存储二进制数据。
Code	|代码类型。用于在文档中存储 JavaScript 代码。
Regular expression	|正则表达式类型。用于存储正则表达式。
## FAQ
- 1 child process failed, exited with error number 100

启动mongodb时，报如下错误：child process failed, exited with error number 100
这是因为非正常关闭mongodb引起的错误，解决办法如下：
删掉以下文件即可(删除数据文件db文件目录下的mongod.lock文件)：/Users/myrna/mongodata/db/mongod.lock
问题解决！
如果还不行，请用管理员权限执行（加`sudo`）

