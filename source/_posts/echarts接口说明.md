---
title: echarts接口说明
date: 2016-09-19 15:02:21
tags: [echarts]
categories: other
---
> The main goal of data visualization is its abliity to visualize data, communicating information clearly and effectively

***
`echarts`是一个基于JS的数据可视化函数库，它不像`jQuery`那样会提供给你一系列的函数去处理
数据，而是提供给你一个配置对象，你可以通过修改这个对象中的内容去控制数据的可视化。

<!-- more -->

# 属性
其中设置对象`option`提供很多属性来方便我们修改可视化图表的情况，下面将依次进行介绍：

#### title
`title`属性是一个对象，它控制了图表的标题，每个图表最多只能有一个`title`对象，可以设定主副两个标题
#### toolbox
`toolbox`属性是一个在图表上提供工具的对象，其中又有`feature`属性控制其中的工具项，工具项有以下几种：

* `mark`：标线

* `dataZoom`：框选区域缩放，会自动与存在的`dataZoom`控件同步

* `dataView`：数据视图，可以设置为只读，用户可以从打开的页面看到所有的数据值，或者指定`readOnly`为`false`打开编辑功能，可以让用用户修改数据值，此时打开的页面会提供刷新按钮，方便用户修改完数据之后刷新图表

* `magicType`：动态类型切换，可以根据当前图表设定可以切换的图表类型

* `restore`：还原，复位为初始图表，可以将用户对图表进行的所有操作进行撤销，使图表变回初始图表

* `saveAsImage`：保存为图片，可以将图表保存为`png`或者`jpeg`格式的图片

#### tooltip
`tooltip`是控制提示框的属性，可以控制鼠标放在图表上的提示框的格式。
其中最主要的属性是`formatter`，可以通过`formatter`属性的模板或者异步回调函数来控制提示框中内容

#### legend
`legend`是控制图例的属性，每个图表最多只能有一个图例，图例中的`data`属性是一个数组，里面包含了图例中的所有项

#### dataRange
`dataRange`是值域选择控件的属性，每个图表最多只能有一个值域控件，可以使用`splitList`属性进行自定义分割，也可以将其置为`null`使用等距比例尺分割

#### dataZoom
`dataZoom`是控制数据区域缩放的属性，与`toolbox.feature.dataZoom`同步，但是此属性仅对直角坐标系的图表有效

#### grid
`grid`属性在官方文档中仅说明是直角坐标系内绘图网格，经过我的测试发现这个属性可以控制直角坐标系图表在整个区域的显示大小和位置，它提供了四个属性来控制这些。

* x：直角坐标系左上角的x轴坐标
* y：直角坐标系左上角的y轴坐标
* x2：直角坐标系右下角的x轴坐标
* y2：直角坐标系右下角的y轴坐标

#### xAxis
`xAxis`是控制直角坐标系横坐标的属性，它的值是一个数组，数组中的每一项代表一条坐标轴，当仅有一条时可以省略数组，当两条坐标轴同时存在时位置互斥。

#### yAxis
`yAxis`是控制直角坐标系纵坐标的属性，它的值是一个数组，数组中的每一项代表一条坐标轴，当仅有一条时可以省略数组，当两条坐标轴同时存在时位置互斥。

#### axis
坐标轴一共有三种类型，类目型、数值型和时间型，它们的区别在于：

* category 类目型：需要指定类目列表，坐标轴内有且仅有这些指定类目坐标
* value 数值型：需要指定数值区间，不指定时则自定计算数值范围，坐标轴内包含数值区间内容全部坐标
* time 时间型：时间型坐标轴用法同数值型，只是目标处理和格式化显示时会自动转变为时间，并且随着时间跨度的不同自动切换需要显示的时间粒度

####  series
`series`是所有属性中最重要的，它是驱动图表生成的属性，它的值是一个数组，数组中的每一项为一系列的选项及数据。
数组中每一项都可能有以下几个属性：

* type：控制生成图表的类型
* name：系列的名称，如果上面启动了`legend`属性，则与`legend.data`索引相关
* data：值是一个数组，为当前系列的图表生成提供数据

#### itemStyle
`itemStyle`属性设置图形的样式，可以分别设置图形的默认样式和强调样式（选中或者悬浮），它的格式如下：
```js
itemstyle: {
    normal: {
		...
	},
    emphasis: {
		...
	}
}
```

#### textStyle
`textStyle`是控制文字样式的属性，其中包含了`color`、`align`、`fontFamily`、`fontSize`等属性控制各种文字的样式

#### other
除以上属性外，`option`中还包含很多其他的属性，如`lineStyle`、`areaStyle`、`loadingOption`等属性



# 方法
`echarts`给我们提供了20个左右的方法，所有的方法都基于`echarts.init()`得到的对象

#### setOption
其中最重要的是`setOption`方法，这个方法是我们使用最多也是每次绘制图表必须使用的方法，这个函数有两个参数：`option`和`notMerge`，其中option就是我们对图表的设置，用来控制图表的生成，`notMerge`参数则是控制本次对图表的设置与上次的`myChart`对象的设置是否进行合并（merge）

#### on&un
`on`方法也是一个比较重要的方法，它的作用是在当前图表对象上添加一个事件监听，它有两个参数分别是字符串`eventName`和方法`eventLintener`，其中`eventName`表示添加的事件类型，`eventLintener`是事件触发后的回调函数，这是一个在实际开发中很有用的函数，可以方便我们对图表点击之类的事件进行响应。
`echarts`给我们提供的`eventName`的事件类型包括：

* 基础事件
 * refresh 刷新
 * restore 还原
 * resize 显示空间变化
 * click 点击
 * dblclick 双击
 * hover 悬浮（获取鼠标焦点）
 * mouseout 鼠标离开图形
* 交互逻辑事件
 * dataChanged 数据修改，如拖拽重定向
 * dataZoom 数据区域缩放
 * dataRange 值域漫游
 * dataRangeHoverLink 值域漫游hover
 * legendSelected 图例选择
 * legendHoverLink 图例hover
 * mapSelected 地图区域选择
 * pieSelected 饼图区域选择
 * magicTypeChanged 动态数据类型切换
 * dataViewChanged 数据视图修改
 * timelineChanged 时间轴变化
 * mapRoam 地图漫游

与`on`方法对应的还有一个`un`方法，这个方法是用来解除添加过的事件绑定，只需要传入事件名称`eventName`即可。

#### getDataURL
`getDataURL`方法是用来获取当前对象的图片格式的，这个方法会返回图片的`base64`编码，这个编码可以直接用来图片显示，也能直接下载。

#### addMarkLine & delMarkLine
`addMarkLine`可以用于在图表已经绘制完成后向图表添加标记线而不重新刷新图表，`delMarkLine`则是删除图表上已经存在的标记线

#### getOption
`getOption`用于向一个已经绘制完成的图表获取它的option的克隆，方便在原来图表的基础上修改部分内容，然后重新绘制图表