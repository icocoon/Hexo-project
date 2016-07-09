---
title: 动态Rem
date: 2016-07-09 19:12:02
tags: [CSS]
toc: false
---
提到`rem`，首先想到的就是字体的设置，类似的比如 px、pt、em等等。

但是`rem`可以做移动端的响应式页面。

<hr>

### 兼容性

在[Can I use](http://caniuse.com/)网站中查询如图所示：
![](http://o768r1c9k.bkt.clouddn.com/Rem%E5%85%BC%E5%AE%B9%E6%80%A7.png)

基本都支持了

### rem

rem是（font size of the root element），根据翻译就是**根据网页的根元素来设置字体大小**，这样一来，就与 em 区别了，em 是根据父元素的字体大小来设置，rem是根据网页的跟元素（html）来设置字体大小的。

>大部分浏览器IE9+，Firefox、Chrome、Safari、Opera ，如果我们不修改相关的字体配置，都是默认显示font-size是16px

所以下列的代码的意思就是给P标签设置12px的字体大小（16*0.75=12）
```css
    p{
        font-size: 0.75em;
    }
```

如果用户自己设置了浏览器的默认字体大小， rem也会跟着用户的调整的大小改变。
**rem不仅可以适用于字体，同样可以用于width height margin这些样式的单位。**

### rem 的数值计算

一般来讲，利用rem来设置css的值，要通过一层计算才行，比如如果要设置一个长宽为100px的div，那么就需要计算出100px对应的rem值是 100 / 16 =6.25rem，这在我们写css中，其实算比较繁琐的一步操作了。

为了方便起见，可以将html的font-size设置成100px，这样在写单位时，直接将数值除以100在加上rem的单位就可以了。

比如：
```css
    html{
        font-size: 100px;
    }

    div{
        width: 4rem;
        height: 4rem;
        background-color: red;
    }
```

上面就创建了一个宽为400px，高为400px，背景颜色为红色的div

### 动态设置 rem 的值

如何动态的设定 rem 的值，使适应不同的设备呢？
可以用 JavaScript 来设置。

```js
    //获取当前设备页面的宽度，赋值给 pageWidth
    var pageWidth = document.documentElement.clientWidth
    //将一个完整的 HTML 的根元素设定字体大小的语句赋值给 content
    var content = 'html{font-size: '+pageWidth/10+'px};'
    //创建一个 style 的标签
    var style = document.createElement('style')
    //将 content 的内容写入 style 标签
    style.innerHTML = content
    //将 style 插入 head 标签内部
    document.head.appendChild(style)
    
```

通过上面的 JS 就能动态的获取到当前页面的宽度，并且写入 head 标签中。


### 栗子

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
  <div class="A"></div>
  <div class="B"></div>
</body>
</html>
```

```css
*{padding:0;margin:0}

div{
  width:5rem;
  height:2.5rem;
  float:left;
}

.A{
  background-color:#f29599;
}

.B{
  background-color:#90c0c0;
}
```

```js
    //获取当前设备页面的宽度，赋值给 pageWidth
    var pageWidth = document.documentElement.clientWidth
    //将一个完整的 HTML 的根元素设定字体大小的语句赋值给 content，注意这里除以10了，所以 1rem 等于十分之一的页面宽度。
    var content = 'html{font-size: '+pageWidth*0.1+'px};'
    //创建一个 style 的标签
    var style = document.createElement('style')
    //将 content 的内容写入 style 标签
    style.innerHTML = content
    //将 style 插入 head 标签内部
    document.head.appendChild(style)
```

上面的代码就创建了两个 div，无论在什么设备都会占据整个页面的宽度，和页面宽度一半的高度。

比如：

<img src="http://o768r1c9k.bkt.clouddn.com/5.png" width=375px height=667px>
<img src="http://o768r1c9k.bkt.clouddn.com/6.png" width=375px height=667px>
<img src="http://o768r1c9k.bkt.clouddn.com/6p.png" width=375px height=667px>





