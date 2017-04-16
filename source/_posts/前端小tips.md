---
title: 前端小tips
date: 2017-3-8
tags: [ css,HTML,Javascript]
categories: 前端
---
> 集腋成裘，聚沙成塔

***
# 说明
这是我在前端使用时遇到各种问题或者小技巧。
# 内容
- json格式中数组的最后一项后面一定不能有逗号
- 页面元素宽度高度是否包含padding和border
	```
默认：不包含
box-sizing:border-box：包含
box-sizing:content-box：不包含
box-sizing:padding-box：只包含padding
	```
- input的cursor属性设为hand会不生效，如果希望放上去是手型，应该设为pointer（目前在chrome浏览器遇到）

js中call方法和apply方法(为了动态改变`this`,两个方法都会改变函数内的`this`指向)：
apply:
	funA.apply(obj,args);
call:
	funA.apply(obj,param1,param2,param3);



css实现多行文本居中
<p data-height="265" data-theme-id="0" data-slug-hash="NpboPe" data-default-tab="css,result" data-user="KIDlfy" data-embed-version="2" data-pen-title="多行文本居中" class="codepen">See the Pen <a href="http://codepen.io/KIDlfy/pen/NpboPe/">多行文本居中</a> by KID (<a href="http://codepen.io/KIDlfy">@KIDlfy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>