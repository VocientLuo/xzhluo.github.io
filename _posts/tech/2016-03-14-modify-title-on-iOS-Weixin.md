---
layout: post
category: tech
tags: tech
keywords: html5 title iOS
description: js修改title在iOS的微信浏览器上不成功的问题
title: js修改title在iOS的微信浏览器上不成功
---

这是在iOS微信上的html5有一个bug，在Android的微信上不存在。
由于微信上的title是native的，因此js修改网页的title不能及时生效，只有跳转到新的页面才能刷新title，所以对于SPA来说很可怕。
有一个黑魔法式的解决方法：

```
document.title = "title";
var $body = $('body');
var $iframe = $('<iframe src="/favicon.ico"></iframe>');
$iframe.on('load',function() {
  setTimeout(function() {
      $iframe.off('load').remove();
  }, 0);
}).appendTo($body);
```

原理是，因为刷新页面时能及时显示title，这个代码就是用iframe做了一次伪请求，在body中添加一个iframe标签，请求成功之后再移除dom，相当于什么也没做，但是页面标题刷新了。
这个解决方法相当酷。
方法来自于网络。