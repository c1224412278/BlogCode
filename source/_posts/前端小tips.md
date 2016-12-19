---
title: 前端小tips
date: 2016-12-3
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