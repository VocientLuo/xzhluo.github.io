---
layout: post
category: tech
tags: tech
keywords: android studio
description: android studio
title: android studio常见问题
---

由于谷歌被墙的原因，android开发官网以及一些开发工具都不能正常使用。
android开发工具android studio安装后会遇到sdk下载失败的问题。
每次打开都会提示 set proxy
在mac下可以通过启动文件设置避开这问题:

* <b>在findler中找到android studio应用程序并显示报内容</b>
like this:
	![image](/images/android_studio_in_findler.png)

* <b>打开Contents/bin/idea.properties文件，在最后加上一行</b>

	``` disable.android.first.run=true ```

保存文件，重新启动 android studio即可。

如果是在windows下就是在安装目录下找到bin目录的idea.properties文件，也是同样的修改即可。

android studio对JDK的依赖是要求版本1.7或者以上。

