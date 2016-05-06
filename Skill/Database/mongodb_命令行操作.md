
# MongoDB 命令行操作

MongoDB 是一种非关系型数据库。经典的关系型数据库有三层结构，database->table->record，
而 mongodb 与相对应的则是datebase->collection->document，如下图所示：

```
+--------+        +----------+
|Database|        | Database |
+--------+        +-----+----+
     |                  |
     |                  |
+----v---+        +-----v----+
| Table  |        |Collection|
+--------+        +----------+
     |                  |
     |                  |
+----v---+        +-----v----+
| Record |        | Document |
+--------+        +----------+
```

## 配置文件 mongodb.conf

- /etc/mongodb.conf 如果没有自己创建一个

```
port=27017  
dbpath=data/db   # 存放数据库的地方
logpath=log/mongodb.log  
logappend=true  
fork=true   # 后台运行
```

` ./bin/mongod -f mongodb.conf `

## 基本操作

本文使用的 MongoDB 版本是 3.2.3。

现在假设我们要创建一个 erp 数据库，然后在 erp 数据库中再创建一个叫 employee 的 collection，
employee 的文档结构示例如下：

```
{
  "name": "Pol",
  "gender": "male"
}
```

下面用 '>' 表示 MongoDB shell 环境，用 '$' 表示终端 shell 环境

- 进入 MongoDB shell

```
# 本地链接，使用默认端口，即 mongo --host 127.0.0.1 --port 27017
$ mongo
# 连接远程数据库
$ mongo --host 100.100.220.75 --port 27017
```

- 查看当前所有的数据库

```
> show dbs
shopping_test   0.002GB
test            0.000GB
```


- 连接数据库

```
> use test
switched to db test
```

- 查看当前连接的数据库

```
> db
test
```

- 查看当前数据库中的所有集合

```
> show collections
user
user_test
```

- 创建新的数据库

在 mongo 中，创建数据库的命令也是 use，比如创建数据库 erp，但是，当我们执行```use erp```时，我们是看不到该数据库的，只有当往数据库插入数据时，它才会显示。执行下面的命令，往数据库中插入两条数据。

```
> db.employee.insert({"name": "Peter", "gender": "male"})
> db.employee.insert({"name": "Lucy", "gender": "female"})
```

## 查找数据

通常情况下，find 方法的第 1 个参数指定查询条件，第 2 个参数指定要返回的字段。

- 显示所有文档数据

```
> db.employee.find({})
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter", "gender" : "male" }
{ "_id" : ObjectId("56dfe2bd42ffea5f73a6af32"), "name" : "Lucy", "gender" : "female" }
```


- 显示第 1 条文档

```
> db.employee.find({}).limit(1)
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter", "gender" : "male" }
```

- 显示 name 为 Lucy 的文档

```
> db.employee.find({"name":"Lucy"})
{ "_id" : ObjectId("56dfe2bd42ffea5f73a6af32"), "name" : "Lucy", "gender" : "female" }
```

- 显示 name 以 P 开头的文档，用到正则表达式，```$options:$i```表示忽略大小写

```
> db.employee.find({'name':{'$regex':'^p', '$options':'$i'}})
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter", "gender" : "male" }
```

- 只显示出 name 的文档，但没有 name 这个 key 的文档也会显示出来，用下面一条命令

```
> db.employee.insert({"gender": "male"})
> db.employee.find({},{"name":1})
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter" }
{ "_id" : ObjectId("56dfe2bd42ffea5f73a6af32"), "name" : "Lucy" }
{ "_id" : ObjectId("56dfe5df3c914ddb65f4f88f") }
```

- 只显示出 name 的文档，且存在这个 name 这个 key

```
> db.employee.find({'name':{'$exists':true}},{"name":1})
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter" }
{ "_id" : ObjectId("56dfe2bd42ffea5f73a6af32"), "name" : "Lucy" }
```

- 按 name 降序排序

```
> db.employee.find().sort({"name":-1})
{ "_id" : ObjectId("56dfe2b742ffea5f73a6af31"), "name" : "Peter", "gender" : "male" }
{ "_id" : ObjectId("56dfe2bd42ffea5f73a6af32"), "name" : "Lucy", "gender" : "female" }
{ "_id" : ObjectId("56dfe5df3c914ddb65f4f88f"), "gender" : "male" }
```


- 导出

如果没有指定导出路径，则默认会在当前路径生成一个 dump 的文件夹。

```
$ mongodump -d erp -c employee
$ mongodump --host 100.103.224.75 --port 17017 -d erp -c items
$ mongodump --host 100.103.224.75 --port 17017 -d erp -c specs -q '{_id: {$gte: ObjectId("50ad7bce1a3e927d690385ec")}}'

dump
└── erp
    ├── employee.bson
    └── employee.metadata.json

$ mongodump -d erp -c employee -o ~/Documents
```

假设想导出最近 1000 条记录，可以这样做：

1.先用命令行排序，查出第 1001 条记录的 _id

```
> db.collection.find('', {'_id':1}).sort({_id:-1}).skip(1000).limit(1)
```

2.假设上面查出的记录的 _id 是 50ad7bce1a3e927d690385ec，然后利用 mongodump 的 -q 选项
进行 dump 数据

```
$ mongodump -d 'your_database' -c 'your_collection' -q '{_id: {$gte: ObjectId ("50ad7bce1a3e927d690385ec")}}'
```

- 导入

- 按原样导入数据库 erp，其中含有一个叫 employee 的 collection

```
$ mongorestore ~/Downloads/dump

2016-03-09T16:32:15.581+0800    building a list of dbs and collections to
restore from /Users/ethan/Downloads/dump dir
2016-03-09T16:32:15.582+0800    reading metadata for erp.employee from
/Users/ethan/Downloads/dump/erp/employee.metadata.json
2016-03-09T16:32:15.582+0800    restoring erp.employee from
/Users/ethan/Downloads/dump/erp/employee.bson
2016-03-09T16:32:15.612+0800    restoring indexes for collection erp.employee from metadata
2016-03-09T16:32:15.613+0800    finished restoring erp.employee (2 documents)
```

- 将 employee 的 collection 导入数据库 test

```
$ mongorestore -d test ~/Downloads/dump/erp

2016-03-09T16:37:21.081+0800    building a list of collections to restore
from /Users/ethan/Downloads/dump/erp dir
2016-03-09T16:37:21.084+0800    reading metadata for test.employee from
/Users/ethan/Downloads/dump/erp/employee.metadata.json
2016-03-09T16:37:21.087+0800    restoring test.employee from
/Users/ethan/Downloads/dump/erp/employee.bson
2016-03-09T16:37:21.148+0800    restoring indexes for collection test.employee from metadata
2016-03-09T16:37:21.148+0800    finished restoring test.employee (2 documents)
2016-03-09T16:37:21.148+0800    done
```

## 更新数据

```
MongoDB 的update 方法的三个参数是upsert，这个参数是个布尔类型，默认是false。当它为true的时候，update方法会首先查找与第一个参数匹配的记录，在用第二个参数更新之，如果找不到与第一个参数匹配的的记录，就插入一条（upsert 的名字也很有趣是个混合体：update+insert）

看下面这个例子：


db.post.update({count:100},{"$inc":{count:10}},true);

在找不到count=100这条记录的时候，自动插入一条count=100，然后再加10，最后得到一条 count=110的记录
```


## Reference

1. [Getting Started with MongoDB (MongoDB Shell Edition)](https://docs.mongodb.org/getting-started/shell/)

2. [Is it possible to mongodump the last “x” records from a collection?](http://stackoverflow.com/questions/7828817/is-it-possible-to-mongodump-the-last-x-records-from-a-collection)

3. [MongoDB 正则表达式](http://www.runoob.com/mongodb/mongodb-regular-expression.html)

4. [Performing regex Queries with pymongo](http://stackoverflow.com/questions/3483318/performing-regex-queries-with-pymongo)

5. [mongodb 的 upsert](http://blog.csdn.net/ayeco/article/details/7300338)


















