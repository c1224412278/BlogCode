---
title: Fate Go 抽卡模拟器
date: 2016-11-19
tags: [FGO,html,jquery,bootstrap]
categories: other
---
> 看天边 霾去雾来

***
# web随机抽卡
&nbsp;&nbsp;经过与小伙伴商讨决定动手写一个web模拟FGO手游抽卡应用。

# 第一版
&nbsp;&nbsp;一开始与一个后端小伙伴决定搭建一个MVC网站模式来实现这个抽卡应用，历时8h左右的时间，我与小伙伴完成了如下工作：

* 数据获取（我）
* 数据处理（小伙伴）
* 前端页面（我）
* 后端算法实现（小伙伴）
* 前后端联调（我&小伙伴）

&nbsp;&nbsp;完成以上工作后，我与小伙伴兴奋的准备上线让群里的小伙伴都体验一下，但是我们遇到了一个最关键的问题**我们没有web服务器**，为了解决这个问题我们做了如下努力：

* 首先小伙伴想到了公司的测试服务器，但是由于项目数量，香港服务器等问题→**失败**
* 其次准备自行购买vps或阿里云服务器，但是由于项目过小后期需要未定→**失败**
* 项目整体重构，全部由前端实现，逻辑代码通过js实现，页面部署在github page上→**成功**

# 第二版
&nbsp;&nbsp;上面说到，由于种种问题，最终整个项目全部被移植到前端实现，所有逻辑代码写在js中，这部分全部由我个人实现，逻辑代码如下：

```js
function getOne() {
    var choose = Math.floor(Math.random() * 100 + 1);
	return choose;
}
function getBaodi() {
	var choose = Math.floor(Math.random() * 20 + 81);
	return choose;
}
function getTen() {
	var list = [];
	for (var i = 0; i < 9; i++) {
		list.push(getCard(getOne()));
	}
	var index = Math.floor(Math.random() * 10);
	list.splice(index, 0, getCard(getBaodi()));
	return list;
}
function getCard(num) {
	var url = "";
	var pond = ALL;
	if(pool == "ALL") {
		pond = ALL;
	} else if(pool == "HALLOWEEN") {
		pond = HALLOWEEN;
	}
	console.log(num);
	console.log(pond);
	switch (true) {
		case num <= 40:
			url = pond.threeauo[(Math.floor(Math.random() * (pond.threeauo.length)))];
			url = url.address;
			break;
		case num > 80 && num <= 83:
			url = pond.fourauo[(Math.floor(Math.random() * (pond.fourauo.length)))];
			url = url.address;
			break;
		case num > 83 && num <= 84:
			url = pond.fiveauo[(Math.floor(Math.random() * (pond.fiveauo.length)))];
			url = url.address;
			break;
		case num > 40 && num <= 80:
			url = pond.threecraft[(Math.floor(Math.random() * (pond.threecraft.length)))];
			url = url.address;
			break;
		case num > 84 && num <= 96:
			url = pond.fourcraft[(Math.floor(Math.random() * (pond.fourcraft.length)))];
			url = url.address;
			break;
		case num > 96 && num <= 100:
			url = pond.fivecraft[(Math.floor(Math.random() * (pond.fivecraft.length)))];
			url = url.address;
			break;
		default :
			url = pond.fiveauo[(Math.floor(Math.random() * (pond.fiveauo.length)))];
			url = url.address;
	}
	return url;
}
```

&nbsp;&nbsp;是一段逻辑十分简单的代码，重点在于业务处理以及数据获取处理部分，在此特别感谢[·Fate/Grand Order中文Wiki主题攻略站 - FGO主题攻略站](https://github.com/ecomfe/echarts)为本项目提供的数据以及图床支持。
&nbsp;&nbsp;逻辑代码处理完成后是页面显示逻辑的处理：

* 首先通过透明度和`z-index`将按钮固定在图片上，借此实现部分图片作为按钮的功能
* 通过图片的相互覆盖实现抽卡之后的图片跳转功能

具体DOM操作如下代码：
```js
    var $one = $(".one-div");
    var $ten = $(".ten-div");
	var pool = $("#class option:selected").text();
	var poolImg = $("#poolImg")[0];
	var url = "stowaway";
    
	$("#class").change(function() {
		pool = $("#class option:selected").text();
		poolImg.src = "http://odqa8xkhb.bkt.clouddn.com/fgo/" + pool + ".jpg";
		$one.fadeOut();
		$ten.fadeOut();
	});
    
	$("#one").click(function() {
		$one.find("img")[0].src=getCard(getOne());
		$ten.hide();
		$one.fadeIn(1000,function() {});
		
	});
    
	$("#ten").click(function() {
		var data = getTen();
	 	data.forEach(function(item, index, arr) {
	 		$ten.find("img")[index].src=item;
	 	});
	 	$one.hide();
		$ten.fadeIn(1000,function() {});
	});
    
	$one.click(function() {
		$one.fadeOut();
		$ten.fadeOut();
	});
    
	$ten.click(function() {
		$one.fadeOut();
		$ten.fadeOut();
	});
```
&nbsp;&nbsp;以上实现了一个简单的Fate/Grand Order（命运冠位指定）游戏的抽卡模拟，现在应用包含`剧情（ALL）`和`玉藻前（HALLOWEEN）`两个卡池（ps：不保证以后的卡池更新）。

[点此抽卡](https://lfy55.github.io/stowaway.html)

**存在的问题：**

* 抽卡没有动画，比较突兀，修复时间未定（划去）以后再说