---
title: React学习笔记01
date: 2016-10-20 10:20:31
tags: React 学习笔记
---
![](http://o768r1c9k.bkt.clouddn.com/react-logo.png)
<!--more-->

## React是什么
狭义来讲，React 是 Facebook 公司内部开源出来的一个前端 UI 框架；
广义来讲，React 不仅仅是 js 框架本身，更是一套完整的前端开发生态系统，这套系统包括了：
1. React.js
2. ReactRenders: ReactDOM / ReactServer / ReactCanvas
3. Flux 模式及其实现（Redux , Fluxxor）
4. React 开源组件
5. React Native
6. GraphQl + Relay

## 基本概念
**React.js**
React.js 是 React 的核心库，在应用中必须先加载核心库。

**ReactDOM.js **
ReactDOM.js 是 React 的 DOM 渲染器，React 将核心库和渲染器分离开了，为了在 web 页面中显示开发的组件，需要调用 ReactDOM.render 方法， 第一个参数是 React 组件，第二个参数为 HTMLElement。

**JSX**
JSX 是 React 自定义的语法，最终 JSX 会转化为 JS 运行于页面当中。

**组件**
组件是 React 中的核心概念，页面当中的所有元素都是通过 React 组件来表达， 我们将要写的 React 代码绝大部分都是在做 React 组件的开发。

**VIRTUAL DOM**
React 抽象出来的虚拟 DOM 树，虚拟树是 React 高性能的关键。

**单向数据流：one-way reactive data flow**
React 应用的核心设计模式，数据流向自顶向下

## Hello React
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <script src="http://facebook.github.io/react/js/react.js"></script>
    <script src="http://facebook.github.io/react/js/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
        var Hello = React.createClass({
          render: function() {
            return <div>Hello {this.props.name}</div>;
          }
        });

        ReactDOM.render(
          <Hello name="World" />,
          document.getElementById('example')
        );
    </script>
  </body>
</html>
```

## React 的独特之处
1. 组件的组合模式
2. 单向数据流的设计
3. 高效的性能
4. 分离的设计

### 组件的组合模式
> 组合模式：组合模式有时候又叫做部分-整体模式，它使我们树型结构的问题中，模糊了简单元素和复杂元素的概念，客户程序可以向处理简单元素一样来处理复杂元素,从而使得客户程序与复杂元素的内部结构解耦。

React 就是基于组合模式， 无论是应用等级还是一个表单亦或是一个按钮都视为一个组件， 然后基于组件的组合构建整个应用，这样的结构一直是前端界想要却迟迟不来的 web component。

基于组合模式的优点：
1. 构建可重用的组件：组件的开发能够形成公司的组件库，每个业务的开发都能积累可重用的组件
2. 无学习障碍：天然符合 HTML 的结构， 对前端开发者来说几乎没有学习障碍
3. 具有弹性的架构：组合模式很简单却很有效，能够构建简单的页面也能构建大型的前端应用。
4. 源码高可维护性：开发只是工作中的一部分，应用的上线才是噩梦的开始，很多大型应用因为复制的业务逻辑导致无法快速响应业务需求，可维护性低。


### 单向数据流的设计
Javascript 是脚本语言，不能像静态语言一样通过编译定位为题，想要清晰的定位到应用中的 bug 需要深入了解业务代码，对于大型前端应用来说，因为业务代码量很大且复杂，很难定位到 bug。 然而 React 的单向数据流的设计让前端 bug 定位变得简单， 页面的 UI 和数据的对应是唯一的,我们可以通过定位数据变化就可以定位页面展现问题。

### 高效的性能
virtual dom，React 之所以能够这样设计要归功于 Virtual DOM 算法， 基于算法可以让只有需要改变的元素才去重渲染。

### 分离的框架设计
React.js 现在的版本已经将源码分开为 ReactDOM 和 React.js . 这就意味着 React 不仅仅能够在 web 端工作， 甚至可以在服务端（nodejs），Native 端运行。

与此同时， 我们可以自定义自己的渲染器， 实现比如 Three.js， Pixi.js， D3.js 的 React 方式渲染。


