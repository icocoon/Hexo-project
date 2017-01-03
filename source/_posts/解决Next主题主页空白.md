---
title: 解决Next主题主页空白
date: 2016-11-14 16:22:39
tags: 随笔
---

今天上来，突然发现博客全部空白了，一个下午的时间都在弄这个。

解决方法：

<!--more-->

由于 GitHub 升级 gitpage，Next 主题下面下 `source/vendors`目录的访问受限

手动将 `source/vendors` 目录修改成 `source/lib` （或者其他的名称，只是 lib 我测试了可以使用）

同时，修改下主题配置文件_config.yml， 将 `_internal: vendors` 改成你所修改的名字，例如  `_internal: lib`

并且修改 next 底下所有引用`source/vendors`路径为`source/lib`

这些地方可以通过文件查找找出来

主要集中在这几个文件中:

1. Hexo\themes\next.bowerrc 
2. Hexo\themes\next.gitignore 
3. Hexo\themes\next.javascript_ignore 
4. Hexo\themes\next\bower.json 。

修改完毕后，刷新重新g一遍就ok啦