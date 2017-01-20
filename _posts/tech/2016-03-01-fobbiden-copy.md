---
layout: post
category: tech
tags: tech
keywords: 禁止复制
description: 网页文本禁止复制
title: 网页文本禁止复制
---

SPA在手机上展示时往往需要页面的文本禁止复制，而通常webview默认是允许长按复制的。

可以通过CSS3属性控制文本禁止复制：

```
 body{
 	-webkit-user-select:none;
 	-moz-user-select:none;
 	user-select:none;
 }
```


