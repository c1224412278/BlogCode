---
title: Hello World
date: 2016-9-18
categories: other
---
***
# 这是我使用github + hexo搭建的个人blog

 blog搭建用了一下午的左右的时间，主要的参考文档是我在`github`上找到的一个[blog](www.ezlippi.com)以及`hexo`的`next`主题
 [如何利用GitHub Pages和Hexo快速搭建个人博客 | Sunwhut's Home](www.ezlippi.com)
 [Next 使用文档](http://theme-next.iissnan.com/)
***
# 问题
在搭建blog过程中也遇到一些问题：

*   首先就是无法使用`hexo deploy`把项目提交到github上，最后通过排查发现是没有确定github的用户名和密码，而我一开始是在git上绑定了我的github信息的，怀疑是SSH配置有误，经过检查发现SSH配置没有错误，最后通过对整个过程的排查发现是`_config.yml`中`deploy`的`repositoty`配置时应该使`ssh地址`而不是`https地址`:
```
deploy:
    repository: git@github.com:lfy55/lfy55.github.io.git
```
*   其次就是如何修改主页显示问题（*暂未解决*）
