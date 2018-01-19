---
title: echarts介绍及使用（三）-4.0新版本特性
date: 2018-1-19
tags: [echarts]
categories: 可视化
---
> 说不定我一生涓滴意念,侥幸汇成河  ——李宗盛

***
# 说明
&emsp;&emsp;时隔一年[ECharts](https://echarts.baidu.com)更新了4.0版本，在我第三天写这篇日志时有迅速放出了4.0.1,4.0.2，也是emmmmmmm。

&emsp;&emsp;也是前段时间年底忙于各种事情，已经快一个月没敲代码了，手都不会打字，以后争取再忙都要敲代码，废话不多说了，看一下echarts的4.0。
# 更新内容
我从echarts官网http://echarts.baidu.com/changelog.html#v4-0-0 截了一张图，看一下4.0究竟干了些什么：

![](http://odqa8xkhb.bkt.clouddn.com/echarts/echarts.4.png)

主要的更新有： 
 - 支持SVG渲染
 - 新增旭日图
 - **新增dataset组件**
 - 支持无障碍富互联网应用规范集

我主要关注的内容有两个SVG渲染和dataset，因为dataset的原因我曾经去看过antv的[g2](https://antv.alipay.com/zh-cn/g2/3.x/index.html)，g2存专门用来处理数据的dataset，可以对数据进行更好的处理和图表联动，下面我将详细介绍一下这两个东西。

# SVG渲染
这个东西，根据官网自己的说法是在移动端少量数据时性能会比Canvas好，但是我基本不在移动端使用echarts，所以就简单尝试了一下，看看以后是否有在PC端使用的情况。
<p data-height="565" data-theme-id="0" data-slug-hash="mpaPNO" data-default-tab="js,result" data-user="KIDlfy" data-embed-version="2" data-pen-title="mpaPNO" class="codepen">See the Pen <a href="https://codepen.io/KIDlfy/pen/mpaPNO/">mpaPNO</a> by KID (<a href="https://codepen.io/KIDlfy">@KIDlfy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

其实只从页面来看并不能区分SVG渲染或者是Canvas渲染，只是对页面性能有些影响，使用方式就是在图表初始化时选中渲染方法：`var chart = echarts.init(document.getElementById('charts'), null, {renderer: 'svg'})`。

# dataset组件
&emsp;&emsp;用于单独的数据集声明,从而数据可以单独管理，可以被多个图表复用，多用于图表联动。echarts官网对于数据集的说法是：
- 数据和其他配置可以被分离开来，使用者相对便于进行单独管理，也省去了一些数据处理的步骤。
- 数据可以被多个系列或者组件复用，对于大数据，不必为每个系列创建一份。
- 更重要的是，有了 dataset 后，能够贴近这样的数据可视化常见思维方式：基于数据（dataset 组件来提供数据），指定数据到视觉的映射（由 encode 属性来指定映射），形成图表。
- 支持更多的数据的常用格式，例如二维数组、对象数组等，一定程度上避免使用者为了数据格式而进行转换。

&emsp;&emsp;这些已经大致总结了dataset的特点，一个简单的例子：
<p data-height="592" data-theme-id="0" data-slug-hash="xpmEVd" data-default-tab="js,result" data-user="KIDlfy" data-embed-version="2" data-pen-title="echarts dataset" class="codepen">See the Pen <a href="https://codepen.io/KIDlfy/pen/xpmEVd/">echarts dataset</a> by KID (<a href="https://codepen.io/KIDlfy">@KIDlfy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

用法：
 - `series.seriesLayoutBy`设置是 dataset 的行还是列映射到 series 上可选值有：`column`(默认值),`row`
 - `encode`来配置数据
    - 维度：当我们把系列（series）对应到“列”的时候，那么每一列就称为一个“维度（dimension）”，而每一行称为数据项（item）。反之，如果我们把系列（series）对应到表行，那么每一行就是“维度（dimension）”，每一列就是数据项（item）
    - 维度的定义：可以使用单独的 dataset.dimensions 或者 series.dimensions 来定义，这样可以同时指定维度名，和维度的类型（dimension type）
    - 维度类型（dimension type）可以取这些值：
        - 'number': 默认，表示普通数据。
        - 'ordinal': 对于类目、文本这些 string 类型的数据，如果需要能在数轴上使用，须是 'ordinal' 类型。ECharts 默认会自动判断这个类型。但是自动判断也是不可能很完备的，所以使用者也可以手动强制指定。
        - 'time': 表示时间数据。设置成 'time' 则能支持自动解析数据成时间戳（timestamp），比如该维度的数据是 '2017-05-10'，会自动被解析。时间类型的支持参见 data。
        - 'float': 如果设置成 float，在存储时候会使用 TypedArray，对性能优化有好处。
        - 'int': 如果设置成 float，在存储时候会使用 TypedArray，对性能优化有好处。
    - x: 将什么维度映射到X轴上，可以指定一个（名称：字符串，序号：number）或者一组数据（数组）
    - y: 将什么维度映射到Y轴上，可以指定一个（名称：字符串，序号：number）或者一组数据（数组）
    - tooltip：将什么数据映射到tooltip展示上
    - seriesName: 将什么数据映射到序列名称

暂时就研究了这么多，等待后续更新