---
layout: post
category: tech
tags: tech
keywords: cordova iOS
description: cordova 打包 ios
title: Mac下Cordova打包iOS
---

在上一篇的基础上，在使demo项目能在ios上运行起来。

1. 准备

	```
	$ npm install -g ios-sim
    $ npm install -g ios-deploy
    ```

    安装这两个插件，参数-g是全局安装。
2. add platform
	切换到demo目录下，因为之前demo项目已经有了cordova android环境
	只需添加ios平台即可。
	```
	cordova platform add ios
	```

3. build
	
	```
	cordova build ios
	```

4. run
	```
	cordova run ios --device
	```

移除平台：
```
cordova platform rm ios
```

cordova的一些设备API是通过插件加载的，比如位置、通知、弹出框、联系人、照相机、媒体库等，具体信息可以查看[这里](http://cordova.apache.org/docs/en/5.1.1/guide/cli/index.html#link-2)

cordova官方文档

[cordova.apache.org/docs](http://cordova.apache.org/docs)