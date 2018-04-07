---
title: echarts介绍及使用（二）-3.x新版本特性
date: 2016-12-26
tags: [echarts]
categories: 可视化
---
> 秋风萧瑟 洪波涌起

***
# 说明
&nbsp;&nbsp;[ECharts](https://github.com/ecomfe/echarts)，是一个我以前介绍过的可视化图表，从一开始我学习的echarts2.2.7版本之后，其官网在10月份升级成了echarts3，因为公司任务一直比较紧，加上最近使用的可视化工具变成了D3，所以没怎么关心。
但在近期做了一个时间不算紧的任务，决定转成echarts3.x做做尝试一下，很久没用不知道，echarts3.x版本确实是一个大更新，而且对比2.x版本有了很多优化，用起来明显舒服了很多。

<!-- more -->
# 内容
下面对echarts3.x版本做一个说明，首先说明一下我用到的跟2.x版本的区别：
1、去除了模块化引入，与2.x版本相比，去除了单种图表的引用，echarts3.x版本全部采用标签式单文件引入，但是你可以自己在[官网-构建js](http://echarts.baidu.com/builder.html)去构建你单文件引入时需要的图表内容，也就是说如果你绘制的图表种类较少的话，相对的你需要引入的文件也会小一些。不仅如此echarts3.x版本的地图数据也没有集成到js文件中，但是你同样可以在[官网-地图构建](http://ecomfe.github.io/echarts-map-tool/)去构建一些常用的地图数据的js或者json文件。
对于3.x版本中的单文件引入方式和地图数据使用方式如下：
```
// 单文件引入
<script src="echarts.min.js"></script>
// js地图数据文件的使用方式
<script src="china.js"></script>
var chart = echarts.init(document.getElementById('map'));
chart.setOption({
    series: [{
        type: 'map',
        map: 'china'
    }]
});
// json地图数据文件的使用方式
$.getJSON('./china.json', function (data) {
        echarts.registerMap('china', data);
        var chart = echarts.init(document.getElementById('map'));
        chart.setOption({
            series: [{
                type: 'map',
                map: 'china'
            }]
        });
    });
```
2、可以使用渐变色来进行图表绘制，渐变色使用的方式如下：
```
color: new echarts.graphic.LinearGradient(
                        0, 0, 0, 1,
                        [
                            {offset: 0, color: '#83bff6'},
                            {offset: 0.5, color: '#188df0'},
                            {offset: 1, color: '#188df0'}
                        ]
                    )
```
其中前四个参数`0,0,0,1`表示渐变方向（范围0~1，相当于在图形包围盒中的百分比，如果最后一个参数传 true，则该四个值是绝对的像素位置），即从(0,0)渐变到(0,1)也就是沿着y轴正方向渐变，第二个数组参数表示渐变的颜色阶段，这个例子中渐变色包含三个阶段。同时也可以通过对象使用渐变色：
```
color: {
    type: 'linear',
    global: false,
    x: 0,
    y: 0,
    x2: 1,
    y2: 0,
    colorStops: [{
        offset: 0, color: 'red'
    }, {
        offset: 1, color: 'blue'
    }]
}
```
3、主题使用更加方便，在[官网-主题构建](http://echarts.baidu.com/download-theme.html)中下载相应主题的js文件，使用方式如下：
```
<script src="echarts.js"></script>
<!-- 引入 vintage 主题 -->
<script src="theme/vintage.js"></script>
<script>
// 第二个参数可以指定前面引入的主题
var chart = echarts.init(document.getElementById('main'), 'vintage');
chart.setOption({
    ...
});
</script>
```

update 2016-12-27
4、dataZoom提供了很多新功能接口：
- zoomLock：可以锁定dataZoom所选择区域
- type：分为`slider`和`inside`两种，其中`slider`是2.x版本中的组件，而`inside`则是将组件内嵌到图表中，可以通过鼠标滚轮来切换dataZoom区间的大小。
- startValue&endValue：接受“绝对数值”的形式定义了数据窗口范围，如果轴的类型为 category，则 startValue 既可以设置为 axis.data 数组的 index，也可以设置为数组值本身。

5、很多图标提供了定制化的选项：
- 可以通过`'image://url'`设置为图片，其中 url 为图片的链接；
- 可以通过`'path://'`将图标设置为任意的矢量路径（`SVG PathData`图标绘制）。这种方式相比于使用图片的方式，不用担心因为缩放而产生锯齿或模糊，而且可以设置为任意颜色。路径图形会自适应调整为合适（如果是`symbol`的话就是`symbolSize`）的大小。