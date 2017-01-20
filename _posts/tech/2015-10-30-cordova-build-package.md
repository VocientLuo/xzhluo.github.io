---
layout: post
category: tech
tags: tech
keywords: cordova
description: cordova 打包
title: Mac下Cordova打包Android
---

1. 准备环境

   	需要有jdk，android SDK
   	并设置相应的环境变量。

2. 安装 cordova

	```
	sudo npm install cordova
	```

3. 创建项目

	创建一个demo文件夹，空的

	```
	cordova create demo com.test.demo demo
	```

4. 把web工程拷贝到demo/www目录下

5. 添加android平台

	```
	cordova platform add android
	```

6. 打包

	```
	cordova build android 
	```

	这时可能会遇到android SDK版本的问题，需要修改几个地方

	1. demo/platforms/android/project.properties
	2. demo/platforms/android/CordovaLib/project.properties
	3. demo/platforms/android/AndroidManifest.xml

	1和2把target变量值改成SDK中已有的版本
	3中的targetVersion的改动也是同一个道理
	改好后再执行 cordova build android

7. 运行

	打开模拟器或者连接设备，使用命令：cordova run android

	如果没处意外，应用就在设备上运行起来了。

	调试插件：

	```
	cordova plugin add https://github.com/jrstarke/webview-debug.git
	```

	调试的时候可以使用，正式发布时需要remove

	```
	cordova plugin remove com.jamiestarke.webviewdebug
	```


cordova官方文档

[cordova.apache.org/docs](http://cordova.apache.org/docs)




