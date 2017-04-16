---
title: css之单行多行文本自动省略及提示全部文字
date: 2017-1-17
tags: [ css,HTML]
categories: css
---

> 学问是经验的积累，才能是刻苦的忍耐

***
# 说明
　　使用纯css实现单行多行文本溢出的自动省略以及跟随鼠标显示所有内容
# 做法

## 单行
我们需要使用`css`提供的一个样式:`text-overflow`,它可以设定三种属性：
- `clip`:直接裁剪，不做任何处理
- `ellipsis`:使用省略号（...）来表示被隐藏的文字
- `String`:使用给定的字符串来表示被隐藏的文字


首先是设置一个`div`用来包裹要省略的文字：
```
<div>
    我太长了，这个该死的作者一定会把我截断的，大家快救救我。
</div>
```
然后是其`css`样式：
```
div {
    /*溢出隐藏*/
    overflow: hidden;
    /*css提供的文字溢出后自动隐藏并显示...*/
    text-overflow: ellipsis;
    width: 200px;
    /*设置文本不换行*/
    white-space: nowrap;
    border: solid 1px red;
}
```
显示效果如下图:

![](http://odqa8xkhb.bkt.clouddn.com/cssTextOverflow/%E5%8D%95%E8%A1%8C%E9%9A%90%E8%97%8F.png)

为其添加鼠标经过显示效果：
首先在`div`标签中增加`tooltip`字段：
```
<div tooltip="我太长了，这个该死的作者一定会把我截断">
    我太长了，这个该死的作者一定会把我截断
</div>
```
`tooltip`字段主要作用是在显示提示的时候知道div中完整的文字。

然后在增加样式：
```
/* 设置提示的显示 */
[tooltip]::before {
    position: absolute;
    top: 20px;
    left: 200px;
    background: #888;
    /* 设置提示中的内容 */
    content: attr(tooltip);
    opacity: 0.0;
}
/* 设置鼠标经过提示的透明度 */
[tooltip]:hover::before {
    opacity: 1.0;
}
```
鼠标经过时如图：

![](http://odqa8xkhb.bkt.clouddn.com/cssTextOverflow/%E5%8D%95%E8%A1%8C%E9%BC%A0%E6%A0%87%E7%BB%8F%E8%BF%87.png)

## 多行
多行情况下只要对div的样式进行一些特别的更改（注意部分属性仅对webkit内核浏览器有效）：
```
div.multi-line {
    /*溢出隐藏*/
    overflow: hidden;
    /*css提供的文字溢出后自动隐藏并显示...*/
    text-overflow: ellipsis;
    width: 200px;
    /*设置webkit浏览器特别的盒模型*/
    display: -webkit-box;
    /*设置文本行数*/
    -webkit-line-clamp: 2;
    /* 设置文本排列方向 */
    -webkit-box-orient: vertical;
    /*设置文本换行属性*/
    word-wrap: break-word;
    word-break: normal;
    border: solid 1px red;
}
```
html代码如下：
```
<div class="multi-line" tooltip="我更长长长长长长长长长长长长长长，我死的更惨惨惨惨惨惨惨惨惨惨">
    我更长长长长长长长长长长长长长长，我死的更惨惨惨惨惨惨惨惨惨惨
</div>
```
显示效果如下图：

![](http://odqa8xkhb.bkt.clouddn.com/cssTextOverflow/%E5%A4%9A%E8%A1%8C.png)
![](http://odqa8xkhb.bkt.clouddn.com/cssTextOverflow/%E5%A4%9A%E8%A1%8C%E9%BC%A0%E6%A0%87%E7%BB%8F%E8%BF%87.png)

# 总结
对于多行的情况目前仅有webkit内核浏览器支持，争取做到所有浏览器支持。