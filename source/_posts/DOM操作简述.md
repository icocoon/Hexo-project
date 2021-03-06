---
title: DOM操作简述
date: 2016-11-21 09:18:04
tags: javascript
---

![](http://o768r1c9k.bkt.clouddn.com/2016-11-19%2016-15-16.png)

DOM原生操作真的很难或者繁琐吗？

[原文链接](https://medium.com/re-dom/master-the-dom-bc1a2a06089b#.54sx1tdxh)
<!--more-->

### 初步介绍

许多web开发者认为DOM真的很难（或者很慢），你需要很多框架来驯服它。
然后他们花了很多时间来学习框架，一两年过去之后，另一个框架变得流行，你需要从头开始学习一切。
这样重复几次，JavaScript疲劳就出现了。更不用说一大堆依赖。

如果我告诉你DOM没有那么难，你会相信吗？如果不需要依赖第三方的库来掌握DOM是不是很酷，你会再给DOM一次机会吗？我们一起来看看


### 创建元素

让我们开始创建HTML元素，为了创建元素，你需要用`document.createElement(tagName)`方法：

```javascript
const h1 = document.createElement('h1')
// <h1></h1>
```

### 修改文本内容
如果html元素没有内容，显示出来就是空的：

```javascript
h1.textContent = 'Hello World'
// <h1>Hello world!</h1>
```

### 添加属性

可以直接添加属性
```javascript
h1.setAttribute('class', 'hello')
// <h1 class="hello">Hello world!</h1>
```

但是如果是为了添加管理类，也可以使用
```javascript
h1.className = 'hello'
// <h1 class="hello">Hello world!</h1>
```

然而，最好的办法还是用classList
```javascript
h1.classList.add('hello')
// <h1 class="hello">Hello world!</h1>
h1.classList.remove('hello')
// <h1>Hello world!</h1>
```

要设置元素的ID,你可以用attribute或者直接设置id属性
```javascript
h1.setAttribute('id', 'hello-world')
h1.id = 'hello-world'
// <h1 id="hello-world" class="hello">Hello world!</h1>
```

>如果你不确定是用attributes还是properties，那就用attributes，除了表单元素的状态，像value和checked


除了下面这些，你不能用element.setAttribute(someBoolean, false)来设置bool值：
```javascript
input.checked = true
// <input checked>
input.checked = false
// <input>
input.setAttribute(‘checked’, ‘’)
// <input checked>
input.removeAttribute('checked')
// <input>
```


### 添加元素
```javascript
document.body.appendChild(h1)
// <body><h1>Hello world!</h1></body>
```


### 删除元素
```javascript
document.body.removeChild(h1)
// <body></body>
```

### 查找元素

+ document.getElementById(id)
+ element.childNodes[i]
+ element.firstChild === element.childNodes[0]
+ element.lastChild === element.childNodes[element.childNodes.length - 1]
+ element.getElementsByTagName(tagName)
+ element.getElementsByClassName(className)
+ element.querySelector(query)
+ element.querySelectorAll(query)

>注意：getElementsByTagName, getElementsByClassName 和 querySelectorAll返回的不是数组，而是一个NodeList，所以不能用ES5的数组迭代器迭代，这里有一些关于[NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList#Workarounds)的介绍

### 元素之间插入元素

```javascript
/*
 *  <body>
 *    <script src="main.js"></script>
 *  </body>
 */
document.body.insertBefore(h1, document.body.firstChild)
/*  <body>
 *    <h1>Hello world!</h1>
 *    <script src="main.js"></script>
 *  </body>
 */
```

### 更新一系列元素

```javascript
const table = document.createElement('table')
document.body.appendChild(table)
updateTable(table, [
  [ 1, 2 ],
  [ 3, 4, 5 ],
  [ 6, 7, 8, 9 ]
])
setTimeout(() => {
  updateTable(table, [
    [ 1, 2, 3, 4 ],
    [ 5, 6, 7 ],
    [ 8, 9 ]
  ])  
}, 1000)
function updateTable (table, data) {
  const rowLookup = table._lookup || (table._lookup = [])
  
  setChildren(table, updateRows(rowLookup, data))
}
function updateRows (rowLookup, rows) {
	return rows.map((row, y) => {
    const tr = rowLookup[y] || (rowLookup[y] = document.createElement('tr'))
    const cellLookup = tr._lookup || (tr._lookup = [])
    setChildren(tr, updateCells(cellLookup, row))
    return tr
  })
}
function updateCells (cellLookup, cells) {
	return cells.map((cell, x) => {
    const td = cellLookup[x] || (cellLookup[x] = document.createElement('td'))
    td.textContent = cell
    return td
  })
}
function setChildren (parent, children) {
  let traverse = parent.firstChild
  for (let i = 0; i < children.length; i++) {
    const child = children[i]
  
    if (child == null) {
      return
    }
  
    if (child === traverse) {
      traverse = traverse.nextSibling
    } else if (traverse) {
      parent.insertBefore(child, traverse)
    } else {
      parent.appendChild(child)
    }
  }
  
  while (traverse) {
    const next = traverse.nextSibling
    parent.removeChild(traverse)
    
    traverse = next
  }
}
```

这里发生了两件事：

+ 这里有一个隐藏的元素`element._lookup = []`，用来查找子元素（可能是一个有id的元素），用这个方法可以重复利用已经存在的dom，更新他们
+ `setChildren(parent, children)`方法里有包含子元素的列表

还可以用setChildren方法来mount/unmount子元素

```javascript
setChildren(login, [
  email,
  !forgot && pass
])
```