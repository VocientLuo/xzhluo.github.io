---
layout: post
category: tech
tags: tech android debug
keywords: android bug fixed
description: Android Studio 运行app时遇到的问题
title: AS在模拟器上调试的问题
---

在使用Android Studio运行app时，编译没什么错，但是安装到模拟器上或者genymotion上时报这样的错误：

```
None of the 1 split apks are compatible with the current device with density 480 and abis x86.

```

在terminal里使用adb install也不行，看这个错误应该是CPU型号不支持，因为工程里有so文件。

与Eclipse不同，遇到这样的错误，Eclipse只要在libs文件夹下建个x86的文件夹，把so文件拷贝过去在run即可。

Android Studio则需要改gradlew文件：

![img](/images/as_nav.png)

找到这个地方：

![img](/images/as_content.png)

这个ndk的对象里加上x86即可。

由于对Android Studio不是很熟悉，这是个很小的问题，但是也纠结了很久。半年不搞安卓，被甩了好几条街。