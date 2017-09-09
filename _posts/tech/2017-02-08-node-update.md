---
layout: post
category: tech
tags: tech
keywords: node update
description: node更新
title: 命令行Nodejs更新
---

先更新npm

```
npm update -g
```

然后安装一个叫'n'的包

```
npm install n -g
```

这个包是专门管理node版本的，安装后执行 n+版本号升级到指定版本

比如：

```
n v4.0
```

也可以直接升级到最新版本

``` 
n latest -g
```

