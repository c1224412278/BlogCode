---
title: node+angular系列（三） - 学习MongoDB.md
date: 2017-1-3
tags: [node,angular,Javascript,mongo]
categories: 前端MVC
---
> 厚积薄发

***
# 说明
　　目标：学习MongoDB NoSQL数据库的使用
　　实现思路：跟随书籍《Node.js+MongoDb+AngularJS Web开发》学习。
# 实现

## 各种命令介绍
- `show users`：列出用户（`db,system.users.find()`）；
- `show dbs`：显示数据库清单
- `use testDB`：切换到数据库（`db = db.getSiblingDb('testDB')`）
- `use newDB`：创建数据库
- `db.dropDatabase`：删除当前数据库
- `show collections`：显示数据库中集合的列表
- `db.createCollection('newCollection')`：创建集合
- `coll.drop()`：删除集合（`coll = db.getCollection('collectionName')`）
- `coll.find(query)`：在集合中查找文档，query是查询条件，使用不带`query`参数的`find()`方法返回集合中的所有文档
- `coll.insert({...})`：将文档添加到集合中
- `coll.remove(query)`：从集合中删除文档，query是查询条件，使用不带`query`参数的`remove()`方法删除集合中的所有文档
- `coll.update({query},{update},{options})`：查询集合中的文档，然后在他们被找到时更新他们，`options`对象中有两个属性`upsert`和`multi`，他们的值全是布尔值，当`upsert`为`true`时，若没找到就创建一个新的文档；当`multi`为`true`时与查询匹配的所有文档都会被更新

## MongoDB+Node.js
使用npm安装MongoDB Node.js驱动程序和Mongoose模块
```
npm install mongodb
npm install mongoose
```

### 使用mongodb包连接数据库（node-mongodb-native）

书上提供了两种使用`mongodb`连接数据库的方法：

1、使用MongoClient对象实例连接到MongoDB
```
var Db = require('mongodb').Db,
    MongoClient = require('mongodb').MongoClient,
    Server = require('mongodb').Server;

  // Set up the connection to the local db
  var mongoclient = new MongoClient(new Server("localhost", 27017), {native_parser: true});

  // Open the connection to the server
  mongoclient.open(function(err, mongoclient) {

    // Get the first db and do an update document on it
    var db = mongoclient.db("integration_tests");
    db.collection('mongoclient_test').update({a:1}, {b:1}, {upsert:true}, function(err, result) {
      assert.equal(null, err);
      assert.equal(1, result);

      // Get another db and do an update document on it
      var db2 = mongoclient.db("integration_tests2");
      db2.collection('mongoclient_test').update({a:1}, {b:1}, {upsert:true}, function(err, result) {
        assert.equal(null, err);
        assert.equal(1, result);

        // Close the connection
        mongoclient.close();
      });
    });
  });
```
但是当我使用时，一直在调用`mongoclient.open()`时报错：`mongoclient.open is not a function`，原因暂时不明，找了很久没找到原因，找到会更新。

2、使用字符串连接到MongoDB
```
var MongoClient = require('mongodb').MongoClient;
MongoClient.connect("mongodb://dbadmin:test@localhost:27107/testDB", function(err, db) {
	// code
});
```
使用这种方法则可以正常连接数据库，其中`mongodb://dbadmin:test@localhost:27107/testDB`中`dbadmin`代表数据库用户账号，`test`代表密码，`testDB`代表数据库名称。

### 使用mongoose包连接数据库
除了通过这两种方法，mongoose包提供了一种更为简单方便的数据库连接方式。
我简单的改造了一下mongoose包官网的例子：
```
// 引入 mongoose 这个模块
var mongoose = require('mongoose');
// 然后连接对应的数据库：mongodb://localhost/testDB，在地址中端口号省略则默认连接 27017；testDB是数据库的名称
// mongodb 中不需要建立数据库，当你需要连接的数据库不存在时，会自动创建一个出来。
// mongodb 的默认配置只接受来自本机的请求，内网都连不上。如果需要在内网中为其他机器提供 mongodb 服务时，可以去看看 iptables 相关的东西。

mongoose.connect('mongodb://localhost/test');


// 创建了一个名为 Dog 的 model，它在数据库中的名字根据传给 mongoose.model 的第一个参数（字符串）决定，mongoose 会将名词变为复数，在这里，collection 的名字会是 `dogs`。
// 这个 model 的定义是，有一个 String 类型的 name，String 数组类型的 friends，Number 类型的 age。
// mongodb 中大多数的数据类型都可以用 js 的原生类型来表示。至于说 String 的长度是多少，Number 的精度是多少。String 的最大限度是 16MB，Number 的整型是 64-bit，浮点数的话，js 中 `0.1 + 0.2` 的结果都是乱来的，就不要指望了。
// 这里可以看到各种示例：http://mongoosejs.com/docs/schematypes.html
var Dog = mongoose.model('Dog', {
  name: String,
  friends: [String],
  age: Number,
});

// new 一个新对象，名叫 tom
// 接着为 tom 的属性们赋值
var tom = new Dog({ name: 'Tom', friends: ['kitty', 'hello']});
tom.age = 5;

// 调用 .save 方法后，mongoose 会去 mongodb 中的 testDB 数据库的Dogs集合中，存入一条记录。
tom.save(function (err) {
  if (err) 
	console.log(err);
});
```
另外你还可以通过`db = mongoose.connection;`来获得一个`Db`对象，并通过以下代码监听数据库连接启动（在调用`mongoose.connect('mongodb://localhost/test');`时数据库连接会自动启动）和错误：
```
db.once('open', function callback () {
  // yay!
});
db.on('error', function callback(err) {
	// code
});
```

### 各种对象及方法

如果是使用mongodb获取的数据库连接则需要各种对象来操作数据库

- DB对象，某一个具体数据库的对象，`Db.dropDatabase`可以删除当前数据库，`db.collectionNames(function(err, collectionNames) {});`可以获得所有的集合名称的数组，`db.collections(function(err, collectionList) {});`则可以获得Collection对象的数组，`myDb.dropCollection("collectionName", function(err, result) {})`和`myDb.collection("collectionName", function(err, collection) { collection.drop();});`都可以删除一个集合。
- Admin对象，对数据库执行某些管理职能可以通过两种方式来得到该对象：`var adminDb = db.admin();`和`var adminDb = new Admin(db)`，使用这个对象可以ping数据库服务器，添加删除用户，列出数据库等，`adminDb.listDatabases(function(err, databases){});`可以获得所有数据库的列表，`adminDb.serverStatus(function(err,status) {})`可以获得数据库的状态;`。
- Collection对象，代表了MongoDB数据库集合，可以通过以下几个方式获得：`var collection = db.collection();`、`var collection = new Collection(db, "collectionName")`、`db.createCollection("collectionName", function(err, collection){});`。
- Cursor对象，当使用MongoDB Nodejs驱动程序在MongoDB中执行某些操作时，结果以Cursor（游标）对象的形式返回，只要使用其each(function(err, item))遍历方法。
