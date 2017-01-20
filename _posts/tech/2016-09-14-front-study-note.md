---
layout: post
category: tech
tags: tech
keywords: 前端学习笔记
description: 前端学习笔记
title: 前端学习笔记
---

## css样式篇

* <b>box-shadow</b>
  
  这个属性是给指定标签的边框加上阴影，增强美化效果。

  属性值为：x y blur spread color inset。
  
| 值 | 含义 |
|----|-----|
| x	  | 必须，x轴方向的值，可以为负值 |
| y   | 必须，y轴方向的值，可以为负值 |
| blur | 可选，模糊的距离 |
| spread | 可选 ，阴影的大小 |
| color | 阴影颜色 |
| insert | 可选，阴影默认为外部阴影，这个值使阴影变成内部阴影 |

一般使用中只要设置x y blur color 就能满足要求。

看个栗子：

写法：```box-shadow: 10px 10px 5px #000000;```

效果1：

![img](/images/box-shadow-1.jpeg)

效果2：

![img](/images/box-shadow-2.jpeg)

* <b>background-position</b>

  背景图片的起始显示位置，一般用于精灵图片，与```background-image```搭配使用，
  
  属性值：x y
  
  | 值 | 含义 |
|----|-----|
| x	  | x轴方向的起始位置，可以为负值，默认0% |
| y   | y轴方向的起始位置，可以为负值，默认0% |

x,y的值可以是像素值，百分比，方位单词(left top right...)。
  
  
  需注意的是，在firefox和opera下需要把```background-attachment```的属性设为```fixed```，否则无效。
  
  看个例子
  
  下面是一张有3个图片的背景图：
  
  ![img](/images/bg-position1.png)
  
  我要在我的div中只显示第一个菱形图或者第二个星星图或者三角形，可以这样写：
  
  ```
  background-image: url(./sources/bg-position.png);
  background-position: -50px -60px;
  ```
  
  效果是这样的：
  
  ![img](/images/bg-position2.jpeg)
  
  再来调整一下x轴方向的位置：
  
  ```
  background-image: url(./sources/bg-position.png);
  background-position: -480px -60px;
  ```
  
  效果如下：
  
  ![img](/images/bg-position3.jpeg)
  
## JS兼容篇

在项目中有个很常见的需求：列表页面滑动到底部时自动加载下一页。

之前在移动端是这么判断页面滑到底部的：

```
window.onscroll = (function(e){
	var scrollTop = document.body.scrollTop;/滚动区高
	var offsetHeight = document.body.offsetHeight;//可见区高
	var domHeight = document.body.scrollHeight;//dom高
	if((scrollTop + offsetHeight) == domHeight){//滑动到了底部
		//TODO
	}
})
```

如果 滚动高度 + 可视区高度 = document的高度，则说明滚动到了底部。

但是有兼容性问题，因为部分浏览器的```document.body.offsetHeight```是把浏览器的边框计算在内的。

所以有时会发现前面两个相加稍微比dom高度大一点。

这里取dom的可见区不应该用```offsetHeight```，而应该使用```document.body.clientHeight```。这样的话就不会有这个问题。

因此我们应该这样使用：


```
window.onscroll = (function(e){
	var scrollTop = document.body.scrollTop;//滚动区
	var clientHeight = document.body.clientHeight;//可见区
	var domHeight = document.body.scrollHeight;//dom高
	if((scrollTop + clientHeight) == domHeight){//滑动到了底部
		//TODO
	}
})
```

但是，这个方法用在移动端是是没问题的，要是用在PC端，我们还有个老古董IE需要兼容。

在IE上，```document.body.scrollTop```这个值会返回0，这时就会懵逼了。

莫急，在IE上我们可以通过另一个对象拿到：```document.documentElement.scrollTop```

因此我们可以这样写：

```var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;```

所以，在任何端都能完美运行的代码就出炉了：

```
window.onscroll = (function(e){
	var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;//滚动区
	var clientHeight = document.body.clientHeight;//可见区
	var domHeight = document.body.scrollHeight;//dom高
	if((scrollTop + clientHeight) == domHeight){//滑动到了底部
		//TODO
	}
})
```
 


	

  
  
  
  