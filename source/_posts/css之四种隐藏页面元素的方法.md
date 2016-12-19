---
title: css之四种隐藏页面元素的方法
date: 2016-11-28
tags: [ css,HTML,bootstrap]
categories: css
---
> **修身**，齐家，治国，平天下

***
# 说明
　　上周六说到使用`css`来隐藏页面元素，当时说存在四种方法，今天就来全部实现一下并且看看区别，方便以后再不同场景下使用。
首先我们先写一个如下页面：
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
	.body {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 600px;
		height: 600px;
		background-color: #999;
	}
	.hidden {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 200px;
		height: 200px;
		background-color: #000;
	}
	</style>
</head>
<body>
	<div class="body">aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
		<div class="hidden"></div>
	</div>
</body>
</html>
```
　　此时页面显示如下：
  ![](http://odqa8xkhb.bkt.clouddn.com/yincang/1start.png)
　　很明显可以看出`.hidden`挡住了`.body`的内容。
# 设置宽度和高度为0
　　将`.hidden`的css样式修改成如下：
```css
.hidden {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 0;
		height: 0;
		background-color: #000;
	}
```
　　此时页面中`.hidden`元素直接消失了，盒模型也说明`.hidden`元素没有在页面上占有位置，通过这种方法隐藏起来的元素有如下特点：

- 大小不存在
- 不在页面上占有位置
- 不耽误下层元素的选中，悬浮等特效

# 设置透明度为0
　　将`.hidden`的css样式修改成如下：

```
.hidden {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 200px;
		height: 200px;
		background-color: #000;
		opacity: 0.0;
	}
```
　　此时页面的显示及盒式模型如下：
![](http://odqa8xkhb.bkt.clouddn.com/yincang/2opacity.png)
　　这时虽然在页面上看不到`.hidden`元素，但是它是确确实实还存于页面上的，它所占的位置还在，只是透明度变成0，所以可以看到下层元素，通过这种方法隐藏起来的元素有如下特点：

- 大小存在
- 在页面上占有位置，会对页面布局起作用
- 会影响下层元素的选中和悬浮等操作

# 设置display为none
　　将`.hidden`的css样式修改成如下：

```
.hidden {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 200px;
		height: 200px;
		background-color: #000;
		display: none;
	}
```

　　此时页面显示如下：
![](http://odqa8xkhb.bkt.clouddn.com/yincang/3display.png)
　　此时对页面也说`.hidden`元素是不存在的，页面上不存在这个元素，通过这种方法隐藏起来的元素有如下特点：

- 不生成盒模型
- 子元素也一样
- 不在页面上占有位置
- 不耽误下层元素的选中，悬浮等特效

# 设置 visibility为hidden
　　将`.hidden`的css样式修改成如下：

```
.hidden {
		position: absolute;
		top: 0px;
		left: 0px;
		width: 200px;
		height: 200px;
		background-color: #000;
		visibility: hidden;
	}
```

　　此时页面显示如下：
![](http://odqa8xkhb.bkt.clouddn.com/yincang/4visibility.png)
　　这种方法与第二种设置透明度的方法只有一个区别，就是它不会影响下层元素的交互事件，通过这种方法隐藏起来的元素有如下特点：

- 大小存在
- 在页面上占有位置，会对页面布局起作用
- 不耽误下层元素的选中，悬浮等特效
- 可以单独显示其子元素

# 总结
　　对四种隐藏元素的方法进行了一遍梳理，以后再需要对页面元素进行隐藏的时候可以选择最合适的方法去使用。
　　今天开始接触`bootstrap`的使用，现在想想我这前端之路也是走的谜一样，而且我对`bootstrap`的认知停留在我可以自己写样式啊，为什么要用这个，这个又不可能存在完全跟设计人员设计的页面一样的控件，还是要我自己写样式去覆盖，用这个有什么意义呢？
　　我觉得随着我前端知识的不断学习，我一定会弄明白这个问题的，毕竟一个如此火的前端框架必定有它的强大之处，我用不好不明白说明我的层次还不够。