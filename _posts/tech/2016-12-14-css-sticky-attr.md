---
layout: post
category: tech
tags: tech
keywords: sticky
description: sticky粘性布局
title: sticky粘性布局
---

### sticky是何物

sticky是CSS3样式中position属性的一个值。

众所周知，position通用的值有：```relatvive```, ```fixed```, ```static```,  ```inherit```值，其作用在w3shool中的介绍如下：

![img](/images/position.png)

我大w2school都没有这个值，那么问题来了，sticky到底是不是position家的？

事实上，sticky确实是position家的，只不过刚出来没多久，还在试行阶段，并不被W3C推荐，因此还没有昭告天下。


### sticky有何用

我们先上[caniuse](http://caniuse.com/)查明一下：

![img](/images/stickyuse.png)

左上角的解释如是说道：

> Keeps elements positioned as "fixed" or "relative" depending on how it appears in the viewport. 
> As a result the element is "stuck" when necessary while scrolling.

大意是其作用是```fixed```和```relative```的合体，既能像fixed一样，恒悬浮在窗口的指定位置，又能像relative一样，具有文档流布局能力。

这简直是为移动端轻应用开发而生，因为这个场景在移动端使用太频繁。比如电商类APP就往往需要随着页面的滚动而动态固定头部的搜索框。

以往我们开发这样的功能可能需要写很多代码，而如果用这个属性可能只需要两三行CSS代码就搞定了，简直是程序猿的春天。

不过别急，上图的大片红色/绿色区域是表示各类浏览器的支持情况，可以看到，目前大部分浏览器都是不支持的。

真是有一把火烧了各浏览器的冲动，这么好的功能竟然不支持，看着Android Browser那栏全是红的就觉得残忍，简直没有人性。

talk is cheap, 抱怨总是没用的。我们还是看看它能给我们解决什么问题。

这里显示iOS上支持比较好，而我们position的fixed属性在iOS上的支持简直是渣渣，原因是iOS在页面滚动时会停止一切js代码运行，而fixed的实现其实也是通过监听浏览器的onscroll方法更新元素位置，使之保持固定在窗口的指定位置，其效果与我们手动绑定onscroll方法更新元素的位置一样的，因此fixed在安卓上使用起来比在iOS上流畅多了，而iOS渣了一地。

至少我们找到了可以解决的方法，我们可以js判断运行环境是iOS还是安卓，动态的设置position的属性，在安卓上用fixed，在iOS上用sticky，这个代码比较简单，略。

实际上我们可以更准确一点，直接判断浏览器是否支持这个属性：

```
function isSupportSticky() {
    var prefixTestList = ['', '-webkit-', '-ms-', '-moz-', '-o-'];
    var stickyText = '';
    for (var i = 0; i < prefixTestList.length; i++ ) {
        stickyText += 'position:' + prefixTestList[i] + 'sticky;';
    }
    // 创建一个dom来检查
    var div = document.createElement('div');
    var body = document.body;
    div.style.cssText = 'display:none;' + stickyText;
    body.appendChild(div);
    var isSupport = /sticky/i.test(window.getComputedStyle(div).position);
    body.removeChild(div);
    div = null;
    return isSupport;
}
```

通过临时创建一个dom元素，并设置该元素的position:sticky属性，在浏览器计算后的样式中是否有改属性。

拥有这个大法，做到全平台超流畅粘性布局，赢取白富美指日可待了。

[参考例子](http://test.nie.163.com/lj/position-sticky.html)

### sticky的使用条件

* 与fixed类似，元素的偏移属性```left,right,top,bottom```至少要有一个有值。而且top和bottom同时设置时，优先对标top，left和right同理，left优先。

* sticky元素的高度/宽度要小于滚动根元素的高度/宽度，也就是说，如果sticky元素比滚动区域还要大，是不生效的。

另外还有一些条件，请直接移步[这里](http://www.tuicool.com/articles/bi6J7nY)吧.

本文的很多知识点也是来自于这位大侠的blog。

总之，sticky的使用环境还是比较苛刻的。

但是我们程序员总是以解决问题为乐。





