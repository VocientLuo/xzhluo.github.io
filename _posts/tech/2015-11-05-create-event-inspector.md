---
layout: post
category: tech
tags: tech
keywords: 组件事件配置器
description: 组件事件配置器
title: 组件事件配置器编写方法
---

与设置器的创建一致，事件配置器的命名规则跟设置器相同。
前缀是相同的，区别在于后缀。
例如：

> 按钮设置配置器：ButtonViewInspector.jsx
> 按钮事件配置器：ButtonViewEventInspector.jsx

都是放在同一个目录下：/static/builder/js/inspectors/
需要在/static/builder/js/Library.js中添加该组件的require代码。

上面的步骤两种配置器是一样的创建方式。
稍微不同的是，事件配置器在Inspector.jsx文件中维护了一份事件配置器表，组件名称 和配置器名称一一对应，所以创建新事件配置器时需要在那里新增该组件的映射。