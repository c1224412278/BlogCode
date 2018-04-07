---
title: echarts介绍及使用（一）
date: 2016-9-19
tags: [echarts,D3,highcharts]
categories: other
---
> 秋风萧瑟 洪波涌起

***
# 简介
&nbsp;&nbsp;[ECharts](https://github.com/ecomfe/echarts)，一个纯 `Javascript` 的图表库，可以流畅的运行在 PC 和移动设备上，兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），底层依赖轻量级的Canvas类库`ZRender`，提供直观，生动，可交互，可高度个性化定制的数据可视化图表。

&nbsp;&nbsp;目前由百度Echarts团队维护，在github社区开源，社区地址为：
```
https://github.com/ecomfe/echarts
```

<!-- more -->
***
# 同类对比
&nbsp;&nbsp;我所了解的可视化图表工具主要有三个`echarts`,`highcharts`,`D3`。他们都能对数据进行可视化操作，但是他们三者又各有不同，三者关系如下：

* echarts我们已经在上面介绍过了
* Highcharts 是一个用纯 JavaScript 编写的一个图表库， 能够很简单便捷的在 Web 网站或是 Web 应用程序添加有交互性的图表，并且免费提供给个人学习、个人网站和非商业用途使用
* D3(Data-Driven Documents)，顾名思义是一种数据驱动文档的JavaScript的函数库，它允许用户绑定任意数据到DOM，然后根据数据来操作文档，创建可交互式的图表

&nbsp;&nbsp;从上图我们可以看出三个图既有相似的地方又有不同之处：

* 三个工具都是基于`JavaScript`的函数库，都是用于数据可视化的工具
* `echarts`和`highcharts`都是一种类似于配置选项自动生成图表的可视化工具（下文会详细说明），而`D3`则需要开发人员使用数据操作DOM进行图表的绘制
* `echarts`和`D3`都是完全开源的，而`highcharts`是一种商务软件，个人和非盈利项目免费，盈利项目收费并提供技术支持，而且`echarts`和`D3`都可以使用标准Geojson格式的地图数据进行地图类图表的绘制，而`highcharts`则需要使用其另一款收费软件`Highmaps`来进行地图相关的绘制
* `highcharts`和`D3`都是基于SVG的图表可视化工具，`echarts`则是基于canvas生成图表
***
# echarts的使用介绍和内部处理流程分析
## 使用
* 首先是echarts的引入，分为模块化包引入、模块化单文件引入、标签式单文件引入三种

* 其次通过`echarts.init()`加载使用的dom，实例化图表对象

* 配置图表设置`option`

* 通过`myChart.setOption()`将配置好的设置加载到图表对象中，然后由echarts自动生成并绘制图表

## 内部处理流程
```
ChartConfig:function(container,option){ …..},//加载Echarts配置文件
ChartDataFormate:{….},//数据格式化
ChartOptionTemplates:{….},//初始化常用的图表类型
Charts:{ RenderChart:function(option){….},//渲染图表
RenderMap:function(option){…}//渲染地图
```
&nbsp;&nbsp;上面的步骤在实际绘图中不会完全的使用到，渲染图表和渲染地图通常只会使用到一种
***
# 图表类型介绍
`echarts`提供的图表类型有十余种：

* **line 折线图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_line.png)
* **bar 柱形图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_bar.png)
* **scatter 散点图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_scatter.png)
* **k K线图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_k.png)
* **pie 饼图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_pie.png)
* **radar 雷达图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_radar.png)
* **chord 和弦图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_chord.png)
* **force 力导向图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_force.png)
* **map 地图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_map.png)
* **heatmap 热力图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_heatmap.png)
* **gauge 仪表盘图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_gauge.png)
* **funnel 漏斗图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_funnel.png)
* **eventRiver 时间河流图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_Event%20River.png)
* **treemap 矩形树图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_treemap.png)
* **venn 韦恩图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_venn.png)
* **tree 树图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_tree.png)
* **wordCloud 字符云图**![](http://odqa8xkhb.bkt.clouddn.com/example_echarts_wordCloud.png)

***
# echarts的简单使用
&nbsp;&nbsp;这里我借助`echarts`官方文档的第一个例子使用最简单的标签式单文件引入的方法简单介绍一下它的使用方法

* 新建一个HTML5页面

```html
<!DOCTYPE html>
<head>
    <mate charset="utf-8">
	<title>Echarts bar</title>
</head>
<body>
</body>
</html>
```
* 在页面中添加一个`<div>`标签用来绘制图表（必须规定宽高）

```html
<!DOCTYPE html>
<head>
    <mate charset="utf-8">
    <title>Echarts bar</title>
</head>
<body>
    <div id="bar" style="height: 400px"></div>
</body>
</html>
```
* 新建`<script>`标签引入标签式单文件`echarts-all.js`

```html
<!DOCTYPE html>
<head>
    <mate charset="utf-8">
    <title>Echarts bar</title>
    <script src="js/dist/echarts-all.js"></script>
</head>
<body>
    <div id="bar" style="height: 400px"></div>
</body>
</html>
```
* 新建`<script>`标签，使用全局变量`echarts`初始化图表并驱动图表的生成

```js
<!DOCTYPE html>
<head>
    <mate charset="utf-8">
	<title>Echarts bar</title>
	<script src="js/dist/echarts-all.js"></script>
</head>
<body>
	<div id="bar" style="height: 400px;width: 600px"></div>
	
    <script>
	var myChart = echarts.init(document.getElementById('bar'));
        
	var option = {
		tooltip: {
			show: true,
			tigger: 'axis'
		},
		legend: {
			data: ['GDP', '人口']
		},
		grid: {
			borderWidth: 0
		},
		xAxis: [
			{
				type: 'category',
				name: '时间',
				axisTick: {show: false},
				splitLine: {show: false},
				data: ['2012', '2013', '2014', '2015']
			}
		],
		yAxis: [
			{
				type: 'value',
				splitLine: {show: false},
				name: '中国GDP(万亿)'
			},
			{
				type: 'value',
				splitLine: {show: false},
				name: '中国人口(万)'
				}
			],
		series: [
			{
				name: 'GDP',
				type: 'bar',
				yAxisIndex: 0,
				data: [534123, 588019, 635910, 676708]
			},
			{
				name: '人口',
				type: 'bar',
				yAxisIndex: 1,
				data: [135404, 136072, 136782, 137325]
			}
		]
	};

	myChart.setOption(option);
	</script>
</body>
</html>
```
&nbsp;&nbsp;通过以上步骤就能成功使用`echarts`绘制出一个双Y轴的柱状图
![](http://odqa8xkhb.bkt.clouddn.com/bar_1.png)

[点此在线预览](http://sandbox.runjs.cn/show/j7bd7ffx)
***
# 小结
&nbsp;&nbsp;这次主要介绍了`echarts`的信息和与其他工具的对比，简要说明了`echarts`的使用方法和内部处理流程，并且完成了一个双Y轴的柱状图demo