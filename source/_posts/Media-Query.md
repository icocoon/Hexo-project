---
title: Media Query
date: 2016-07-06 20:04:59
tags: [CSS]
toc: false 
---

Media Query，即[CSS 媒体查询](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries)，包含了一个媒体类型和至少一个媒体属性来限制样式表范围的表达式。

### 如何引用 Media Query

1. 在 `<link>`标签上使用：
```CSS
<link rel="stylesheet" media="(max-width:1000px)" href="XXX.css">
```

**注意，即使 CSS 不满足 Media Query 的条件，也会被下载下来**

2. 在 CSS 代码中使用
```
    @media (max-width:1000px){
        CSS代码块
    }
```

### 逻辑操作符

and，not，only 可以用来构造复杂的 Media Query

1. and 操作符用来把多个媒体属性组合起来，合并到同一条媒体查询中。**只有当每个属性都为真时，这条查询的结果才为真。**
    ```CSS
    <!--举个栗子：下面这条媒体查询仅在电视媒体上，可视区域不小于700像素宽度并且是横屏时有效-->
    @media tv and (min-width: 700px) and (orientation: landscape) { ... }
    ```
2. not 操作符用来对一条媒体查询的结果进行取反。**注意，是对一条媒体查询的结果，也就是说，要先媒体查询筛选，然后取反，最后才计算 not**
    ```CSS
        @media not all and (monochrome) { ... }
    <!--等价于-->
        @media not (all and (monochrome)) { ... }
    ```
3. only 操作符表示仅在媒体查询匹配成功的情况下应用指定样式（就是老旧的浏览器不认识 CSS3 的一些属性，就不会去执行后面的 CSS 文件，专门给老旧的浏览器使用的，老浏览器只要看到 only ，就不会应用样式）。
```CSS
    <link rel="stylesheet" media="only screen and (color)" href="example.css" />
```

### 逗号分隔列表
媒体查询中使用逗号分隔效果等同于 or 逻辑操作符。当使用逗号分隔的媒体查询时，**如果任何一个媒体查询返回真，样式就是有效的。**
```CSS
    @media (min-width: 700px), handheld and (orientation: landscape) { ... }
```
如上文，如果是一个800像素宽的屏幕设备，媒体语句将会返回真，因为第一部分相当于 @media all and (min-width: 700px) 将会应用于该设备并且返回真，尽管我的屏幕媒体类型并不与第二部分的手持媒体类型相符。同样地，如果我是一个500像素宽的横屏手持设备，尽管第一部分因为宽度问题而不匹配，第二部分仍会成功，因此整个媒体查询返回真。

### 几个重要概念
1. 物理像素：就是实实在在的像素点，屏幕上的一个小圆点代表一个像素，这是物理决定的
2. 设备独立像素（虚拟像素，密度无关像素）：比如有一些视网膜屏，则会用4个物理像素，去表示原来的一个像素，这样会更细腻，更清楚，比如苹果的 Retina 屏幕
3. 设备像素比（DPR）：设备像素比 = 物理像素/虚拟像素

JavaScript 中可以用`window.devicePixelRatio`获取当前屏幕的设备像素比
CSS 中可以用`-webkit-device-pixel-ratio`获取当前屏幕的设备像素比


### 媒体属性

>大多数媒体属性带有“min-”和“max-”前缀，用于表达“小于等于”和“大于等于”。这避免了使用与HTML和XML冲突的“<”和“>”字符。如果你未向媒体属性指定一个值，并且该特性的实际值不为零，则该表达式被解析为真。

1. 颜色（color）
2. 颜色索引（color-index）
3. 宽高比（aspect-ratio）
4. 设备宽高比（device-aspect-ratio）
5. 设备高度（device-height）
6. 设备宽度（device-width）
7. 网格（grid）
8. 高度（height）
9. 黑白（monochrome）
10. 方向（orientation）：landscape（横向） portrait（纵向的）
11. 分辨率（resolution）
12. 扫描（scan）
13. 宽度（width）

### 测试媒体查询
>DOM有这样一种特性，可以通过程序来获得媒体查询的结果。这是通过 `MediaQueryList` 接口和它的方法来实现的。一旦你创建了`MediaQueryList` 对象， 你就可以通过它来检查查询结果

在获取查询结果前，你先要创建 `MediaQueryList` 对象来存放媒体查询。
为了实现这个目的，需要使用`window.matchMedia`方法。

举个例子，比如你想设置一个查询列表用来判定设备屏幕处于横屏还是竖屏，那你可以像下面这样编码：
```JavaScript    
var mql = window.matchMedia("(orientation:portrait)")

if(mql.matches){
    console.log("设备屏幕处于竖屏")
} else {
    console.log("设备屏幕处于横屏")
}
```



