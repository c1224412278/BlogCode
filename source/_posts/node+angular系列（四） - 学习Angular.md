---
title: node+angular系列（四） - 学习Angular
date: 2017-2-7
tags: [node,angular,Javascript,mongo]
categories: 前端MVC
---
> 水滴石穿

***
# 说明
　　目标：学习Angular相关内容
　　实现思路：跟随书籍《Node.js+MongoDb+AngularJS Web开发》学习。

  <!-- more -->
# 实现
Node版本：v4.5.0
Angular版本：v1.2.32

## 全局API

| 实用程序        | 说明          |
| ------------- |:-------------:|
| copy(src, [dst]) | 创建src对象或者数组的深拷贝[赋值给dst] |
| element(element) | 返回一个jQuery元素的DOM元素，是一个jquery对象或者子集 |
| equals(o1,o2) | 通过`===`比较o1和o2两个对象 |
| extend(dst,src) | 从src对象复制所有属性到dst对象 |
| forEach(obj,iterator,[context]) | 遍历obj(对象，数组)集合中的每个对象，iterator是一个要调用的函数，包含value和key两个参数，context指定充当上下文，是在循环中通过`this`来访问的JavaScript对象 |
| fromJson(jsonStr) | 从一个JSON字符串返回一个JavaScript对象 |
| toJson(jsonObj) | 返回JavaScript对象的JSON字符串格式 |
| isArray(value) | 判断参数value是否是一个数组 |
| isDate(value) | 判断参数value是否是一个Date对象 |
| isDefined(value) | 判断参数value是否是一个已经定义的对象 |
| isElement(value) | 判断参数value是否是一个DOM元素对象或jQuery对象 |
| isFunction(value) | 判断参数value是否是一个JavaScript函数 |
| isNumber(value) | 判断参数value是否是一个数值 |
| isObject(value) | 判断参数value是否是一个JavaScript对象 |
| isString(value) | 判断参数value是否是一个String对象 |
| isUndefined(value) | 判断参数value是否是`undifined` |
| lowercase(string) | 返回参数string的小写版本 |
| uppercase(string) | 返回参数string的大写版本 |


## 过滤器

### 过滤器使用方法

1、可以在视图表达式中使用:
```
{{expression | filter}} //单个过滤器的使用
{{expression | filter | filter}} //可以把多个过滤器链接在一起，他们将按照指定好的顺序执行
{{expression | filter:parameter1:parameter2}} //有些过滤器可以提供输入
```
2、使用依赖注入添加过滤器，这些是控制器和服务的提供器：
```
// 使用特定的过滤器
controller('myController', ['$scope', 'currencyFilter', function($scope, currencyFilter) {
	$scope.getCurrencyValue = function(value) {
		return currencyFilter(value, "$USD");
	}
}]);
// currencyFilter被添加到用于控制器的依赖注入中，并作为一个函数调用

// 使用过滤器集合 $filter
controller('myController', ['$scope', '$filter', function($scope, $filter) {
	$scope.getCurrencyValue = function(value) {
		return $filter('currency')(value, "$USD"); // $filter('currency') == currencyFilter
	}
}]);
```

### Angular内置的过滤器('/'代表'|',markdown语法冲突)

| 过滤器        | 说明          |
| ------------- |:-------------:|
| currency[:symbol] | 使用所提供的的symbol值把数字格式设置为货币，如果没有提供symbol值，则使用为该地区默认的符号，例如：&#123;&#123;123.46 / currency:"$USD"}} |
| filter:exp:compare | 使用exp参数的值，根据compare值过滤表达式，例如：&#123;&#123;"Some Text to Compare" / filter:"text":false }} |
| json | 把一个JavaScript对象格式化成JSON字符串，例如：&#123;&#123; &#123;'name':'Brad'} / json }} /
| limitTo:limit | 由limit值限制表达式中所表示的数据。如果表达式是一个String，则限制字符数，如果表达式是一个Array，则显示元素数目，例如：&#123;&#123; ['a', 'b', 'c', 'd'] / limitTo:2}} |
| lowercase | 输出转换成小写的结果，例如：&#123;&#123; 'aBcDe' / lowercase }} |
| uppercase | 输出转换成大写的结果，例如：&#123;&#123; 'aBcDe' / lowercase }} |
| number[:fraction] | 把数值格式化为文本。如果指定了fraction参数，那么其大小限制所显示的小数的位数(四舍五入)，例如：&#123;&#123; 123.456789 / number:3 }} |
| orderBy:exp:reverse | 根据exp参数对数组排序，exp参数可以是一个函数，它计算数组中的一个条目的值；或者是一个字符串，它指定对象数组一个对象属性。reverse参数为true表示降序，为false表示升序，例如：&#123;&#123; [&#123;'id':1},&#123;'id':3},&#123;'id':2}] / orderBy:'id':true }} |
| data[:format] | 使用format参数格式化JavaScript Date对象、时间戳或日期ISO 8601的日期字符串，例如：&#123;&#123; 1389323623006 / date: 'yyyy-MM-dd HH:mm:ss Z'}} |

### 自定义的过滤器

AngularJS提供了`filter()`方法来创建一个过滤器提供器，并把它注册到依赖注入的服务器。
```
filter('myFilter', function() { // 创建一个名为myFilter的过滤器
	retrun function(input, param1, param2) {
		return <<modified input>>;
	};
});
```

## Angular指令

指令部分中自带的指令都是比较常用的指令，自己定义指令部分看的云里雾里，不是很清楚，暂时先不写关于这方面的东西。

## AngularJS服务

