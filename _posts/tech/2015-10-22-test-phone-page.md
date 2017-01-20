---
layout: post
category: tech
tags: tech
keywords: chrome 测试 kaifa 
description: 
title: 手机网页联机调试
---

chrome和safari都支持远程调试，以chrome为例，我们只需这样操作：

1. 手机连接电脑，并打开开发者模式；

2. 打开PC上的chrome；

3. 在地址栏里输入 ``` chrome://inspect ``` ，回车；

   ![img](/images/chrome_inspect.png)

4. 手机chrome打开要调试的网页，在PC上的chrome就会出现手机上打开的网页地址。
   ![img](/images/chrome_test_url.png)
   点击地址下方的inspect即可进行远程调试。

注：chrome第一次调试时PC联网需要翻墙，以后不需要。否则点击inspect出现的是空白页，什么也没有的。

