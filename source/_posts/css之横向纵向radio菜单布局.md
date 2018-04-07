---
title: css之横向纵向radio菜单布局
date: 2017-2-22
tags: [ css,HTML]
categories: css
---

> 学问是经验的积累，才能是刻苦的忍耐

***
# 说明
　　使用css实现radio的横向纵向布局菜单单选以及inline-block样式引起的空白解决方案

<!-- more -->
# 做法

## 横向
不多说，贴代码：
```
<div id="menu">
    <input type="radio" name="myColor" id="aaaa" checked="checked">
    <label class="menu-label" for="aaaa">
        aaaa</label>
    <input type="radio" id="bbbb" name="myColor"><label class="menu-label" for="bbbb">
        bbbb</label>
    <input type="radio" id="vvvv" name="myColor"><label class="menu-label" for="vvvv">
            vvvv</label>
    <input type="radio" id="dddd" name="myColor">
    <label class="menu-label" for="dddd">dddd</label>
</div>
```

然后是其`css`样式：

```css
<style>
    input {
        display: none;
        width: 0px;
        height: 0px;
        margin: 0px;
        padding: 0px;
    }
    label {
        width: 100px;
        height: 30px;
        /*margin-right: -0.25em;  *//* 不是完全适应，不推荐 */
        display: inline-block;
        line-height: 30px;
        text-align: center;
        border: 1px solid #054ffd;
        cursor: pointer;
    }
    input:checked+label {
        background: #ddd;
    }
</style>
```

显示效果如下图:

![](http://odqa8xkhb.bkt.clouddn.com/cssRadioMenu/horizontal+spack.png)

很明显可以看出每两个label中都存在一些空隙，在dom元素中又看不到这些空隙，为了消除这些空隙，解决方法有三种：

1. 在label标签中设置margin-right:-0.25em;
2. 将lebel标签和input标签中的回车去除，即标签间不换行
3. 使用jquery从其父元素中将其同级且nodeType为3的元素删除，具体代见下文js
```js
$('#menu').contents().filter(function () {
    return this.nodeType === 3;
}).remove();
```

非常不推荐使用方法一，当自己书写html页面时可以使用方法二，方法三使用起来也比较方便，同时我们可以通过jquery看一下这个空格到底是什么，
首先我们使用方法三，然后在filter函数中增加一句`console.log(this)`，这时候页面效果如图：

![](http://odqa8xkhb.bkt.clouddn.com/cssRadioMenu/horizontal.png)

这时候控制台输出如下：

![](http://odqa8xkhb.bkt.clouddn.com/cssRadioMenu/console.png)

可以看出来这些空格在控制台输出中也是一些空格，它的`nodeType`等于3，我们只需要将它们删掉就行了

## 多行

只需要将`label`标签的样式改为如下格式即可：
```css
label {
    width: 100px;
    height: 30px;
    display: block;
    line-height: 30px;
    text-align: center;
    border: 1px solid #054ffd;
    cursor: pointer;
}
```

这时显示效果如下图：

![](http://odqa8xkhb.bkt.clouddn.com/cssRadioMenu/vertical.png)

# 总结

以前使用绝对定位方式来做这种效果，这样对元素的个数等有很大的限制，现在换成这种方式，暂时还没有发现存在有什么问题，发现了会更新的。。。
