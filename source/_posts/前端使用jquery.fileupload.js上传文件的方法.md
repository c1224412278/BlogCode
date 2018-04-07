---
title: 前端使用jquery.fileupload.js上传文件的方法
date: 2016-11-30
tags: [ css,HTML,Javascript]
categories: 前端
---
> **修身**，齐家，治国，平天下

***
# 说明
　　最近需要在前端做一个可以批量上传文件的功能，决定使用[jquery.fileupload.js](https://github.com/blueimp/jQuery-File-Upload)插件来实现相关功能。

<!-- more -->
# 普通上传
　　通过[官方github](https://github.com/blueimp/jQuery-File-Upload)和[参考博客](http://www.cnblogs.com/mafeifan/p/3291562.html)，得出一个最普通的文件上传网页。
  首先，通过git clone的文件结构如图：
  ![](http://odqa8xkhb.bkt.clouddn.com/fileup/file%20tree.png)
  自己创建一个web服务项目，将server和js文件夹复制进去，server文件夹中的后端脚本可以只保留php，然后创建一个index.html页面，内容是：
  ```
  <!DOCTYPE HTML>
<html>
<head>
<meta charset="utf-8">
<title>jQuery File Upload Example</title>
<style>
.bar {
    height: 18px;
    background: green;
}
</style>
</head>
<body>
<input id="fileupload" type="file" name="files[]" data-url="server/php/" multiple>
<script src="js/jquery-3.1.0.js"></script>
<script src="js/vendor/jquery.ui.widget.js"></script>
<script src="js/jquery.iframe-transport.js"></script>
<script src="js/jquery.fileupload.js"></script>
<script>
$(function () {
    $('#fileupload').fileupload({
        dataType: 'json',

        // 上传完成后的执行逻辑
        done: function (e, data) {
            console.log(data);
            $.each(data.result.files, function (index, file) {
                $('<p/>').text(file.name).appendTo(document.body);
            });
        },

        // 上传过程中的回调函数
        progressall: function (e, data) {
            console.log("loaded:"+data.loaded + ",total:" + data.total);
            var progress = parseInt(data.loaded / data.total * 100, 10);
            console.log("progress:" + progress);
            $(".bar").text(progress + '%');
            $('#progress .bar').css(
                'width',
                progress + '%'
            );
        }
    });
});
</script>

<!-- 进度条 -->
<div id="progress">
    <div class="bar" style="width: 0%;"></div>
</div>
</body>
</html>
  ```
  这样就实现了一个简单的文件上传页面。
  # 调整页面显示
  上面的网页上传前和上传后界面分别如图：
  ![](http://odqa8xkhb.bkt.clouddn.com/fileup/0start.png)
  
  ![](http://odqa8xkhb.bkt.clouddn.com/fileup/0end.png)
  现在存在的问题有：
  - 自动上传
  - 界面不够友好
  对于第一个问题只要添加一个`button`，然后通过这个按钮来触发上传事件即可。
# 更新1202
更换插件，选择[fileup](https://github.com/haggen/fileup)插件进行上传。