---
layout: post
category: tech
tags: tech
keywords: android studio 依赖配置
description: 
title: android studio中项目依赖出错
---

在用android studio开发中开发安卓时遇到一个依赖报错的问题：

```
Error:(7, 13) Failed to resolve: com.android.support:appcompat-v7:23.2.1
<a href="install.m2.repo">Install Repository and sync project</a><br><a href="openFile:/Users/vocient/work/enterprise/project/ent_plus/UnifyApp/build.gradle">Show in File</a><br><a href="open.dependency.in.project.structure">Show in Project Structure dialog</a>
```
 
就是 ```appcompat-v7``` 这个包没找到

在android studio中的包依赖与eclipse不一样，eclipse是要把jar包放到libs下作为依赖引用，as更加智能，只要在build.gradle中添加依赖记录即可，as会自动去找，找不到时会提示，可以根据提示下载完成。

这里我跟着提示去下载这个依赖，结果还是报错，提示说sdk目录下的一个文件夹已经存在，目录是：

```
sdk/extras/android/m2repository/
```

报错是已经存在，我先备份一下，然后删除该目录，再重新安装这个依赖，就可以了。

回头再来看一下这个目录：

![img](/images/as_support_lib.png)

这应该是存放安卓sdk额外的一些包的目录，这些包不是sdk所必须，但是又经常会用到的。

我的as开始会报错的原因是这个文件夹已经存在了，但是又没有 ```appcompat-v7``` 这个包，而点击安装时是安装整个包仓库。因此出现上面的情况。

