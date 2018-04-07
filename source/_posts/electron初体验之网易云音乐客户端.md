---
title: electron初体验之网易云音乐客户端
date: 2017-10-13
tags: [vue, electron, webpack]
categories: js
---
> 纸上得来终觉浅，绝知此事要躬行

# 初始化一个electron项目

<!-- more -->
## 使用electron-vue构建

```
vue init simulatedgreg/electron-vue my-project
```

### 使用electron-packer 进行打包

```
electron-packager . --platform=win32 --arch=x64 --electron-version=1.6.8  --overwrite
```


## 使用 electron-builder 打包
```
npm config set electron_mirror http://npm.taobao.org/mirrors/electron/
```

执行上一步之后会在`C:\Users\sqk_5\AppData\Local\electron-builder\cache\nsis-resources`中生成一些文件

`electron-builder`可以再`build`目录下打包出一个`.exe`文件


使用`electron-builder`时`build\win-unpacked\resources`目录下会生成一个`app.asar`的压缩文件，这个文件包含了项目的内容，用来进行项目构建，这时需要在`package.json`文件中使用`main`指定`app.asar`中的渲染`js`文件，使用`electron-vue`则为：`dist/electron/main.js`。

> tips:
>
> 压缩解压asar文件流程：
>
> 首先安装：`npm install -g asar`
>
> 打包命令：`asar pack your-app app.asar`
>
> 解压命令：`asar extract app.asar app`

我使用electron-vue脚手架以及[网易云音乐接口](https://github.com/Binaryify/NeteaseCloudMusicApi)编写了一个[网易云音乐客户端](https://github.com/lfy55/NeteaseCloudMusic)，第一次做electron项目，很丑功能也不多，做的不好请轻喷。
