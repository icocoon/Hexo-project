---
title: Ajax
date: 2016-07-02 23:32:17
tags: [前端]
toc: false
---

ajax：一种请求数据的方式，只需要局部刷新页面，技术核心是 XMLHttpRequest 对象

ajax 的请求过程：创建XMLHttpRequest 对象、连接服务器、发送请求，接受响应数据

### 创建
IE7及其以上的版本支持原生的 XHR 对象，因此可以直接用：
```js
var xhr = new XMLHttpRequest();
```

IE6及其以下的版本，可以使用：
```js
ar xhr =new ActiveXObject(’Microsoft.XMLHTTP’);
```

### 连接与发送
open()函数有三个参数，请求方式，请求地址，是否异步请求（True，False）**一般不用同步**

请求方式中，get 是通过 URL 参数将数据提交到服务器，**而 post 则是将数据作为 send 函数的一个参数提交给服务器**

而且 post 请求中，在发送数据之前，要设置表单提交的内容类型

### 接收
接收响应后，响应的数据会填充 XHR 对象，相关属性如下：

`responseText`：响应返回的主题内容，为 string 类型
`reponseXML`：如果响应类型是"text/xml"或者"application/xml"，这个属性中将保存着相应的 XML 数据，是 XML 对应的 document 类型
`status`：响应的 http 状态码，状态码以2开头的都是成功，304表示从缓存中获取
`statusText`：响应的 http 状态的说明

XHR 对象的`readyState`属性表示请求/响应过程的当前活动阶段，这个属性的值如下
0-未初始化，尚未调用open()方法；
1-启动，调用了open()方法，未调用send()方法；
2-发送，已经调用了send()方法，未接收到响应；
3-接收，已经接收到部分响应数据；
4-完成，已经接收到全部响应数据；

只要 `readyState` 的值变化，就会调用 `readystatechange` 事件

>ajax请求是不能跨域的！


<hr>


**具体代码如下**
get
```js
function loadDoc(){
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function(){
        if (xhr.readyState == 4 || xhr.status == 200) {
            document.getElementByID('demo').innerHTML = xhr.responseText;
        }
    }
    xhr.open('get',url,true);
    xhr.send();
}
```
post
```js
function ajaxpost(){
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function(){
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log(xhr.responseText)
        }
    };
    xhr.open('post',url,true);
    xhr.setRequestHeader('content-type');
    xhr.send('name=xxx&phone=xxx')
}
```

**注意 post 要加上 setRequestHeader()**
其中 'name=xxx&phone=xxx' 这种类型的就叫做 urlencoded

