---
title: js之在jQuery选择器中选择js对象
date: 2017-1-18
tags: [ js,HTML]
categories: js
---

> 学问是经验的积累，才能是刻苦的忍耐

***

# 说明
在公司代码中看到一段很神奇的`jQuery`动画的代码:
```
$({value: 0}).animate({value: 180}, {
    duration: 3000,
    step: function(now,fn) {
        // ....
    }
});
```
其中`step`函数会在动画执行过程中不断的执行，`now`参数则在value值从0变成180过程中的数字。

我研究了一下通过这种方法可以控制一个元素在一段时间内的动画，甚至在一段时间内多个不同元素同时进行动画，并且保证多个元素的动画都是同步的。

<!-- more -->
# 做法
首先我做了一个测试，代码如下:
<p data-height="265" data-theme-id="0" data-slug-hash="WRoWdG" data-default-tab="result" data-user="KIDlfy" data-embed-version="2" data-pen-title="WRoWdG" class="codepen">See the Pen <a href="https://codepen.io/KIDlfy/pen/WRoWdG/">WRoWdG</a> by KID (<a href="http://codepen.io/KIDlfy">@KIDlfy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
在动画执行的过程中页面上会显示一个从0-180的浮点数，fn则是代表动画中的对象的各种属性，通过控制台输出它的值如下：
```
init
    easing:"swing"
    elem:Object
    end:180
    now:59.54019145893518
    options:Object
    pos:0.3307788414385288
    prop:"value"
    start:0
    unit:"px"
    __proto__:Object
```
# 总结
原理暂时不明，等我研究一下，继续更新。
以后简单代码可以托管在[codepen](https://codepen.io/)中，这样方便阅读博客时去运行调试代码。