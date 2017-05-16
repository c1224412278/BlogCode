---
title: ES6之set&map
date: 2017-5-16
tags: [ Javascript,es6]
categories: 前端
---
> 学如逆水行舟，不进则退

***
# 说明
通过学习[ES6 标准入门（第二版）--阮一峰](es6.ruanyifeng.com)书籍和[在线网站](es6.ruanyifeng.com),学习ES6标准，同时记录学习笔记

# SET
类似于数组但是成员是唯一的（加入值时不会进行类型转换，计算是否相等的算法类似`===`）

## 构造方法：
var s = new Set();
可以接受一个数组（或者类似数组的对象）进行初始化（重复部分会舍去）

## 实例的属性：
	size:实例的成员数

## 实例的数据结构：
```
{
	size: 4,
	[[Entries]]: [1,2,3,4],
	__proto__:{}
}
```

## 实例的操作方法：

- add(value): 添加一个值，返回实例本身
- delete(value): 删除一个值，返回一个布尔值表示删除是否成功
- has(value): 判断一个值是否在实例内，返回一个布尔值
- clear(): 清除所有成员，没有返回值，实例变为一个空Set对象

> ps:Array.from方法可以将Set结构转化为数组（var arr = Array.from(set)）

> pps: 简单的数组去重的方法：
function dedupe(array) {
    return Array.from(new Set(array));
}
	
## 实例的遍历方法：

- keys(): 返回键名的遍历器
- values(): 返回键值的遍历器（Set的键与值相同，所以keys和values方法的返回值一致）
- entries(): 返回键值对的遍历器
- forEach(): 使用回调函数遍历每个成员

> ps: 或者直接使用for...of遍历Set