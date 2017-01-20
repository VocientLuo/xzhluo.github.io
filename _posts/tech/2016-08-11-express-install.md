---
layout: post
category: tech
tags: tech
keywords: express nodejs
description: 安装express应用后无法使用的问题
title: express command not found
---

使用nodejs创建一个express应用时，要先安装express。

我们习惯会这样做：

```
npm install express
```

或者这样：

```
npm install -g express
```

可是安装完成之后键入express命令时会有这样的提示：

```
-bash: express: command not found
```

一开始以为会是没安装上，可是又没报错，而其实express使用不是直接安装express，而是安装express-generator

要这样做：

```npm install -g express-generator``` 

或者这样做：

```npm install express-generator```
