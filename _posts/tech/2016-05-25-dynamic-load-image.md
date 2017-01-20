---
layout: post
category: tech
tags: tech
keywords: js动态加载图片
description: js动态加载图片
title: js动态加载图片
---

与移动端的native图片加载不同，native的图片加载、大小处理、显示全靠自己手动完成。而html历史悠久，因此在屏幕显示图片很智能。

只要告诉img标签，图片地址在哪里，即可完成图片加载、处理和显示，整个图片下载和图片大小处理全不用管。

但这个智能同事也限制了移动端的表现。移动端不像PC端，有足够的空间提供图片处理，因此在移动端的img标签就显得不尽如意。

特别是列表式的图片显示，看上去就很糟糕。

尽管如此，万能的程序员都总是有办法的，且看我们的移动端html5的列表图片优化策略。

我们先看看native的图片加载：

![img](/images/native-image-show.png)

native图片加载，一般都有这样几个原则：

* 屏幕外的图片不加载

* 屏幕滑动时不加载

* 图片加载进行压缩处理

* 图片加载后进行缓存

native显示一张图片要做这么多工作。再看我们html5的图片显示：

![img](/images/web-image-show.png)

虽然简单粗暴，但是跟native在移动端比性能就差远了。

不过我们对比上面的方式，我们也可以借鉴一下native的加载。

native在图片加载完成前一半是显示一张本地默认图片，等图片下载完成、处理好后替换默认图片。

因此我们web端也可以这么干。原理大概是这样：

* 第一步 我们先把img标签的src属性放置一张早就加载好的图片，把真实的图片放到一个自定义属性里，比如data-src；

* 第二步 找出在屏幕内的img标签，并逐一将属性data-src的值放到src属性里；

* 第三步 监听dom滑动，并在监听里执行第二步

这样一来，大大减小了单位时间内的图片加载负担，提升了体验。

参考实例：

[https://github.com/dcloudio/mui](https://github.com/dcloudio/mui)

[https://github.com/barretlee/lazyload](https://github.com/barretlee/lazyload)


