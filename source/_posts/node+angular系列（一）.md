---
title: node+angular（一）——为什么是node和angular
date: 2016-12-19
tags: [node,angular,Javascript,mongo]
categories: 前端MVC
---
> 不进则退

***
# 说明
　　目标：学习node和angular的使用，理解前端mvc的含义
　　实现思路：跟随书籍《Node.js+MongoDb+AngularJS Web开发》学习。

<!-- more -->
# 实现
## 为什么是node
> node.js是一个基于谷歌的V8 JavaScript引擎，并执行该引擎的开发框架。

node 的优点：
- JavaScript端至端：可以同时使用JavaScript进行客户端和服务器端脚本的编写。
- 事件驱动的可扩展性：使用一种基本的事件模型在同一线程上处理（单线程）。
- 可扩展性：社区活跃，包管理器npm方便使用。
- 快速执行：node跑一个web服务器特别方便、速度。

## 为什么是MongoDB
> MongoDB是一个灵活和可扩展性非常好的NoSQL数据库。

MongoDB的优点：
- 针对文档：MongoDB是针对文档的，数据在数据库中存储的格式，非常接近在服务器和客户端脚本中处理他们的格式。
- 高性能：MongoDB是目前性能最高的数据库之一。
- 高可用性：MongoDB的复制模型使得它能够很容易维护可扩展性，同时保持高性能。
- 高可扩展行：MongoDB的结构使得它可以很容易地通过在多个服务器上对数据分片。

## 为什么是Express
Express模块在套件中充当web服务器，它的优点有：
- 路由管理：Express可以很容易地定义直接绑在服务器上的Node.js脚本功能的路由（URL端点）。
- 错误处理：Express为“未找到文件”等错误提供了内置的错误处理。
- 易于集成：一个Express服务器可以很容易地在现有的反向代理系统，使你可以轻松地将它集成到现有的安全系统。
- cookie：Express提供了简单的cookie管理。
- 回话和缓存管理：Express也能够进行会话管理和缓存管理。

## 为什么是AngularJS
AngularJS是谷歌开发的客户端框架，它背后的理论是提供一个框架，使得可以很容易地实现使用MVC框架的Web应用程序。
它的优点有：
- 数据绑定：其具有强大的范围机制，有一个将数据绑定到HTML元素的非常干净的方法。
- 可扩展性：允许你轻松地扩展语言的各个方面，以提供你自己的自定义实现。
- 整洁：AngularJS迫使你编写干净的、合乎逻辑的代码。
- 可重用代码：可扩展性和和简洁的代码的结合，使得很容易用AngularJS编写可重用的代码。
- 支持：谷歌的大力支持。
- 兼容性：AngularJS基于JavaScript并与JQuery有着密切的关系。

# 总结
今天暂且先看看这本书使用的技术和它们的优点，并简单的看下书的内容，以后会随着书本进行项目的编写。