---
layout: post
category: tech
tags: tech
keywords: appbricks 组件
description: appbricks新增组件
title: 在appbricks中新增组件
---

基于IDE开发组件，包括四部分：

* 组件样式

* 配置器样式

* 组件

* 配置器

这四个部分分别对应IDE中的的两个目录结构：

``` 
|- less/
|   |
|   -- builder/
|	|		|-- inspectors/		
|   |
|   -- runtime/
|	|		|-- components/
|- static/
|   |
|   -- builder/
|	|		|-- js/
|	|		|	  |-- inspectors/
|   |
|   -- runtime/
|	|		|-- js
|	|		|	  |-- components/

```

样式放在less目录下，组件样式放在less/runtime/components/下，设计器样式放在less/builder/inspectors下；
组件和设计器放在static的runtime和builder对应的文件夹下。
另外还需要添加引用这些样式和组件、设计器的代码。
在less/builder/builder.less文件中添加引用设计器样式的代码：

```
@import 'inspectors/inspectors-name'

```

同理在less/runtime/runtime.css中添加类似代码

组件和设计器的引用：
组件：
在static/runtime/js/library.js中添加：

```
require('./components/componentName');

```

设计器：
在static/builder/js/Library.js中添加：

```
require('jsx!./inspectors/InspectorName');

```


