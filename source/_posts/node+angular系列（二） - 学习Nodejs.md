---
title: node+angular系列（二） -  学习Nodejs
date: 2016-12-22
tags: [node,angular,Javascript,mongo]
categories: 前端MVC
---
> 厚积薄发

***
# 说明
　　目标：学习node的使用
　　实现思路：跟随书籍《Node.js+MongoDb+AngularJS Web开发》学习。
# 实现
Node版本：v4.5.0

## npm包管理器
查看当前项目包含的包的版本命令：`npm version`
npm命令如下：
| 选项        | 说明           | 示例  |
| ------------- |:-------------:| -----:|
| search      | 在存储库中查找模块包 | npm search express |
| install      | 使用在存储库或本地位置上的一个package.json文件来安装包      |   npm install <br />npm install express<br />npm install express@0.1.1<br />npm install ../Module.tgz  |
| install -g | 在全局可访问的位置安装一个包     |    npm install express -g |
| remove | 删除一个模块      |    npm remove express |
| pack | 把在一个package.json文件中定义的模块封装成.tgz文件      |    npm pack |
| view | 显示模块的详细信息      |   npm view express  |
| publish | 把在一个package.json文件中定义的模块发布到注册表     |    npm publish |
| unpublish | 取消一个你已经发布的包      |    npm unpublish express |


## package.json文件
创建一个需要express模块作为依赖的模块时，package.json的内容是：
```
{
	"name": "module_name",
	"version": "0.0.1",
	"dependencies": {
		"express": "latest"
	}
}
```
##  创建一个Node.js程序

1、创建一个文件夹
2、在文件夹中创建一个名为censortext.js的文件
3、在censortext.js文件中添加如下代码：

```
var censoredWords = ["sqk","lfy"];
var customCensoredWords = [];

function censor(inStr) {
	for(idx in censoredWords) {
		inStr = inStr.replace(censoredWords[idx],"***");
	}
	for(idx in customCensoredWords) {
		inStr = inStr.replace(customCensoredWords[idx], "---");
	}
	return inStr;
}

function addCensoredWord(word) {
	customCensoredWords.push(word);
}

function getCensoredWords() {
	return censoredWords.concat(customCensoredWords);
}

exports.censor = censor;
exports.addCensoredWord = addCensoredWord;
exports.getCensoredWords = getCensoredWords;
```

4、要生成Node.js封装模块，需要创建一个package.json的文件，其中至少添加name(名称)，version（版本）和main指令。main指令需要是被加载的主JavaScript的模块的名称，在这个例子中是consortext。需要注意的是`.js`不是必须的，Node.js会自动搜索`.js`扩展名。package.json文件内容是：
```
{
	"author": "lei feiyu",
	"name": "censotify",
	"version": "0.1.0",
	"description": "Censors words out of text",
	"main": "consortext",
	"dependencies": {},
	"engines": {
		"node": "*"
	}
}
```

5、在文件夹下创建一个名为README.md的文件，在这个文件中可以写一些说明。
6、在控制台导航到你创建的文件夹中，然后执行`npm pack`命令建立一个本地封装模块。

update 2016-12-29 继续学习