---
layout: post
category: tech
tags: tech
keywords: node node-inspector
description: 使用node-inspector调试node服务端代码
title: 使用node-inspector调试node服务端代码
---

* 安装node-inspector

```
npm install -g node-inspector
```

* 启动node-inspector

```
node-inspector
```

启动之后会有

> Node Inspector v0.12.8
> Visit http://127.0.0.1:8080/?port=5858 to start debugging.

的提示，只要在浏览器访问这串地址就可以；

* 开启服务
比如coffee就用：

```
coffee --nodejs --debug runtime-server.coffee
```

启动后，就可以在浏览器里看到后台的代码了。可以跟前端代码一样调试。