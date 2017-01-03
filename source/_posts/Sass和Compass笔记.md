---
title: Sass和Compass笔记
date: 2016-12-16 14:17:44
tags: [CSS]
toc: false
---

![Sass](http://o768r1c9k.bkt.clouddn.com/sass-logo-wall.jpg)

<!--more-->

# Sass

## 介绍
sass是一种"CSS预处理器"，可以让CSS的开发变得简单和可维护。

## 安装与使用

### 安装
sass是Ruby语言写的，但是两者的语法没有关系。不需要懂得 Ruby 也可以使用 Sass。
安装 Ruby 后，执行：

```
gem install sass
```

### 使用
sass就是普通的文本文件，里面可以直接使用CSS语法。文件后缀名是.scss，意思为Sassy CSS。

>关于使用这一块，阮一峰老师的[SASS用法指南](http://www.ruanyifeng.com/blog/2012/06/sass.html)很详细的介绍了，所以不再累述。

# Compass

![](http://o768r1c9k.bkt.clouddn.com/compass-squashed.png)

之所以写这篇博客，是因为最近学到 compass，发现意外的好用，为了以后的方便，所以写下使用的步骤。

## 介绍

简单说，Compass是Sass的工具库，Sass本身只是一个编译器，Compass在它的基础上，封装了一系列有用的模块和模板，补充Sass的功能。

## 安装
Compass也是用Ruby语言写的，所以安装它之前，必须安装Ruby。

安装 Ruby 后，执行：
```
sudo gem install compass
```

## 使用

### 创建

命令行中 cd 到想要使用的位置，执行：
```
compass create test
```

看到
```
Congratulations! Your compass project has been created.
```
就代表创建完成了
![](http://o768r1c9k.bkt.clouddn.com/compass-create-squashed.png)

当前目录中就会生成一个 test 子目录

进入该目录：

![](http://o768r1c9k.bkt.clouddn.com/compass-test.png)

test 下面有三个文件：

1. config.rb文件，这是你的项目的配置文件
2. sass，存放Sass源文件
3. stylesheets，存放编译后的css文件

### 编译
我们需要知道如何编译，因为不能够直接使用 scss 文件。
我们写出来的是后缀名为 scss 的文件，只有编译成 css 文件，才能用在网站上。

Compass的编译命令是：
```
compass compile
```

该命令在项目根目录下运行，会将sass子目录中的scss文件，编译成css文件，保存在stylesheets子目录中。

但是这个命令编译出来的 css 文件带有大量的注释，而一般生产环境则需要压缩后的 css 文件，所以我们使用：
```
compass compile --output-style compressed
```

**在命令行模式下，除了一次性编译命令，compass还有自动编译命令**

```
compass watch
```

运行该命令后，只要scss文件发生变化，就会被自动编译成css文件。


## compass模块
compass 内置有5个模块：
* reset
* css3
* layout
* typography
* utilities


### reset模块
reset模块重置浏览器的默认样式，写法是：
```
@import "compass/reset";
```

>但是有更好的重置浏览器的默认样式的方法，就是使用 compass-normalize

使用 compass-normalize，首先要安装：
```
gem install compass-normalize
```

然后要做的就是引入插件，在 config.rb 文件的最上方，使用 require 引入

```
require 'compass-normalize'
```
这样一来就不需要引入reset模块了。


### css3模块
支持 css3 特性，举个栗子：
圆角的写法是：
```
@import "compass/css3";
　　.rounded {
　　　　@include border-radius(5px);
　　}
```

@include命令，表示调用某个mixin（类似于C语言的宏），5px是参数，这里用来指定圆角的半径。
编译后的代码为:

```css
.rounded {
　　　　-moz-border-radius: 5px;
　　　　-webkit-border-radius: 5px;
　　　　-o-border-radius: 5px;
　　　　-ms-border-radius: 5px;
　　　　-khtml-border-radius: 5px;
　　　　border-radius: 5px;
　　}
```

### 其他模块
其他模块见[官方文档](http://compass-style.org/)


## Helper函数
除了模块，Compass还提供一系列函数。
有些函数非常有用，比如`image-width()`和`image-height()`返回图片的宽和高。
其他见[官方文档](http://compass-style.org/)