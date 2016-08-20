---
title: React基础学习笔记
date: 2016-08-07 10:08:51
tags: [前端]  
toc: false 
---

![](http://o768r1c9k.bkt.clouddn.com/react-logo.png)


注：本篇笔记来源于 阮一峰 老师的博客 [React 入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html)
<!--more-->
### react结构模板
如果要使用 react ，网页源码的结构大致如下：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React demo</title>
     <script src="http://obkhl70m6.bkt.clouddn.com/react.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/react-dom.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/browser.min.js"></script>
</head>
<body>
    <div id="example"></div>

    <script type="text/babel">
        代码
    </script>
</body>
</html>
```

上面代码需要注意两点：
1. body 中的 js 代码区域，标签 `script` 中的 type 必须为`text/label`。
2. 代码使用了三个库，`react.js`、`react-dom.js`、`browser.min.js`，这三个库是使用 react 必须要加载的三个库。

>三个库的链接：
>http://obkhl70m6.bkt.clouddn.com/react.js
>http://obkhl70m6.bkt.clouddn.com/react-dom.js
>http://obkhl70m6.bkt.clouddn.com/browser.min.js


### ReactDOM.render()
ReactDOM.render() 是 react 的最基本的方法，**用于将模板转化为 HTML 语言，并插入指定的 DOM 节点**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React demo</title>
     <script src="http://obkhl70m6.bkt.clouddn.com/react.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/react-dom.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/browser.min.js"></script>
</head>
<body>
    <div id="example"></div>

    <script type="text/babel"> <!--注意是 babel 而不是 label-->
        ReactDOM.render(
            <h1>Hello World</h1>, <!--注意有一个逗号-->
            document.getElementById('example') 
        )
    </script>
</body>
</html>
```

上述代码，将一个 h1 标签，插入了 example 节点中。
[栗子效果](http://obkhl70m6.bkt.clouddn.com/React01.html)

### JSX 语法
上一节的代码， HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React demo</title>
     <script src="http://obkhl70m6.bkt.clouddn.com/react.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/react-dom.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/browser.min.js"></script>
</head>
<body>
    <div id="example"></div>
    
    <script type="text/babel">
        var name = ['Alice','Emliy','Kate'];

        ReactDOM.render(
            <div>
                {
                    name.map(function(name){
                        return <div>Hello,{name}</div>
                    })
                }
            </div>,
            document.getElementById('example')
            <!--注意 id 的 d 为小写-->
        )
    </script>
</body>
</html>
```

[栗子效果](http://obkhl70m6.bkt.clouddn.com/React02.html)

JSX 的基本语法规则：
1. **遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析**。
2. **JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React demo</title>
     <script src="http://obkhl70m6.bkt.clouddn.com/react.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/react-dom.js"></script>
    <script src="http://obkhl70m6.bkt.clouddn.com/browser.min.js"></script>
</head>
<body>
    <div id="example"></div>
    
    <script type="text/babel">
        var arr = [
            <h1>JSX 的语法规则</h1>,
            <h2>允许插入变量</h2>,
            <h2>如果变量是数组，则展开显示这个数组的所有成员</h2>,
        ];

        ReactDOM.render(
            <div>{arr}</div>,
            document.getElementById('example')
        );
    </script>
</body>
</html>
```
[栗子效果](http://obkhl70m6.bkt.clouddn.com/React03.html)

2016-08-08号 未完待续
















