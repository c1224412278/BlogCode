---
title: js 跨域相关内容
date: 2017-10-17
tags: [js, cors]
categories: js
---
> 纸上得来终觉浅，绝知此事要躬行

# 跨域相关内容
<!-- more -->
## JSONP方式

`jsonp`方式是一种`hack`模拟`script`标签的方式，具体使用方式如下：
```
function do(data) {
    console.log(data)
}
var script = document.createElement('script')
script.src = 'http://www.xxx.com/query?keyword=aaa&callback=do'
document.body.appendChild(script)
```
服务端响应如下（express）：
```
let cb = req.query['callback']
res.send(cb + '("jsonp")');
```
浏览器输入如下：
```
"jsonp"
```

这种方法需要window对象下面定义回调函数，只支持`get`方法，但是可以兼容所有浏览器

## CORS方式
CORS(Corss-origin resource sharing)，跨域资源共享，是一个W3C标准，它允许浏览器向跨域服务器发起`XMLHttpRequest`请求。

浏览器会将CORS请求分成两种：简单请求和非简单请求
只要同时满足一下两个条件就是简单请求，否则是非简单请求：
1. 请求方法是一下三种方法之一：
    - HEAD
    - GET
    - POST
2. HTTP的头信息不超出一下几种字段：
    - Accept
    - Accept-Language
    - Content-Language
    - Last-Event-ID
    - Content-Type:只限于三个值：`application/x-www-from-urlencoded`,`multipart/from-data`,`text/plain`

### 简单请求

对于简单请求浏览器会直接发出CORS请求，但是会在请求头中添加一个`Origin`字段，只要服务器在响应头中添加一个`Access-Control-Allow-Origin`字段，并且其中包括请求的域就可以完成一次跨域请求。

### 非简单请求

浏览器会先进行一次`HTTP`查询请求(`OPTIONS`方式)，被称为"预检"请求(preflight)，当预检请求通过后才会发出真正的请求。

预检请求会包含以下请求头：
- `Accept-Control-Request-Headers`:CORS请求需要的头信息
- `Accept-Control-Request-Methed`:CORS请求的方法

服务器在收到预检请求时需要提供以下响应头使浏览器能够通过预检并发出真正的请求，为了保证浏览器通过预检，预检请求的响应头需要包括以下内容：
- `Accept-Control-Allow-Origin`:(必须)服务器允许的域，必须包含请求的域
- `Accept-Control-Allow-Methods`:(必须)服务器允许的方法，通常包含:`GET`,`POST`,`PUT`,`DELETE`,`OPTIONS`
- `Accrpt-Control-Allow-Metheds`:(不必须)如果预检请求中包括`Accept-Control-Request-Headers`字段，则相应头则必须包含当前字段，且当前字段要包括请求的所有值
- `Accept-Control-Allow-Credentials`:(不必须)表示是否允许发送`Cookie`，只能设置为`true`表示允许，不设置则表示不允许，如果要发送`Cookie`请求也要设置`withCredentials`为`true`
- `Accept-Control-Max-Age`:(可选)指定本次预检的有效期，在此期间不需要再次预检

参考文档：
> [跨域资源共享CORS详解 -- 阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)