---
title: CSS动画
date: 2016-07-11 09:33:10
tags: [CSS]
toc: false
---

关于Transition、Transform、Animation。

<!--more-->

### 一些 API
1. Transition 过渡
2. Transform 变形
3. Animation 动画

### 以前的动画
以前一般都是用雪碧图，调整 left 使得图片使用视觉暂停原理，变成动画。
方法：
1. 可以使用 JS 改变图片的 left 值
2. 使用 jQuery 的 $.animate 改变 left 值

而现在的则是纯的像素变化，效率是非常高的
**语法：一般是 Animation 中使用 @keyframes（关键帧）**

### Transition
从一个状态，到另一个状态。

![Transition](http://o768r1c9k.bkt.clouddn.com/Transition.png)

Transition 就是在初始状态和结束状态的中间，创建过渡动画。

**注意，Transition 使得 dom 的值真的变化了，因为有结束状态，会自动计算中间的状态值**

完整语法：
```css
.example {
    transition: [transition-property] [transition-duration] [transition-timing-function] [transition-delay];
}
```

分别是：
过渡属性名 transition-property
过渡持续时间 transition-duration
过渡时间函数 transition-timing-function
过渡推迟时间 transition-delay

其中过渡推迟函数可以在 chrome 浏览器中看到
![transition-timing-function](http://o768r1c9k.bkt.clouddn.com/transition-timing-function.png)

<img src="http://o768r1c9k.bkt.clouddn.com/transition-timing-function2.png" width=375px height=667px>

[查看可以使用Transition的属性](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties)

### Transform

语法：一般是

```css
div {
    transform:rotate(7deg);
}
```

常用变换：

| 值 |         描述          |
|-----|:----------------------|
|none  |  定义不进行转换|
|translate(x,y)  |  定义 2D 转换|
|translate3d(x,y,z) |   定义 3D 转换|
|translateX(x)  |  定义转换，只是用 X 轴的值|
|translateY(y) |   定义转换，只是用 Y 轴的值|
|translateZ(z) |   定义 3D 转换，只是用 Z 轴的值|
|scale(x,y)  |  定义 2D 缩放转换|
|scale3d(x,y,z)  |  定义 3D 缩放转换|
|scaleX(x) |   通过设置 X 轴的值来定义缩放转换|
|scaleY(y) |   通过设置 Y 轴的值来定义缩放转换|
|scaleZ(z) |   通过设置 Z 轴的值来定义 3D 缩放转换|
|rotate(angle)  |  定义 2D 旋转，在参数中规定角度|
|rotate3d(x,y,z,angle)  |  定义 3D 旋转|
|rotateX(angle)  |  定义沿着 X 轴的 3D 旋转|
|rotateY(angle) |   定义沿着 Y 轴的 3D 旋转|
|rotateZ(angle)  |  定义沿着 Z 轴的 3D 旋转|
|skew(x-angle,y-angle)  |  定义沿着 X 和 Y 轴的 2D 倾斜转换|
|skewX(angle)  |  定义沿着 X 轴的 2D 倾斜转换|
|skewY(angle)  |  定义沿着 Y 轴的 2D 倾斜转换|
|perspective(n)  |  为 3D 转换元素定义透视视图|


### Animation

语法：一般是

```css
@keyframes changeColor{
  from{background:#ddd}
  to{background:#e6637c}
}

div{
  height:100px;
  width:100px;
  background:#ddd;
  animation:changeColor 5s;
}
```

**注意：先声明在使用**
```css
animation: name duration timing-function delay iteration-count direction;
```


| 值 |         描述          |
|-----|:----------------------|
|animation-name            |  规定需要绑定到选择器的 keyframe 名称|
|animation-duration         | 规定完成动画所花费的时间，以秒或毫秒计|
|animation-timing-function  | 规定动画的速度曲线|
|animation-delay            | 规定在动画开始之前的延迟|
|animation-iteration-count  | 规定动画应该播放的次数|
|animation-direction        | 规定是否应该轮流反向播放动画|

**animation-iteration-count: infinite 表示播放无限遍**
**animation-direction: alternate 表示交替播放**

[查看更多请到 MDN CSS Animations](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations)























