---
title: node+angular系列（三） - 学习MongoDB.md
date: 2017-1-1
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