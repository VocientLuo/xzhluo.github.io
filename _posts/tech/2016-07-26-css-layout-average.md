---
layout: post
category: tech
tags: tech
keywords: css 前端
description: css 均分父容器宽度
title: css均分父容器宽度
---

在前端布局开发中，我们通常会遇到这样的需求：

![img](/images/layout_weight.png)

一个容器视图里有多个水平排列的子视图，这些子视图是均分父容器的宽度。

我们可以在css中给定RootView的宽度，比如```width:100%```，然后给定每个子View的宽度为平均宽度。

这样是可以满足一部分需求的。

但如果有更进一步的需求：我们需要根据api的数据来控制这里的子视图的个数。

当然我们可以通过js动态计算每个子View的宽度，但是那样显得很麻烦。

是时候挖掘我们强大的css样式了。

css中display有一个table-cell的值，可以达到我们的需求。

html代码如下：

```
<div class="table">
  <div class="table-cell">cell1</div>
  <div class="table-cell">cell2</div>
  <div class="table-cell">cell3</div>
  <div class="table-cell">cell4</div>
</div>
```

css代码如下：

```
.table{
	width:100%;
	display:table;
}
.table-cell{
	display: table-cell;
	width:1%;
	text-align: center;
	border: 1px solid #eee;
	height:30px;
	line-height: 30px;
}
```

效果图：

![img](/images/layout_cell.png)

这里必须指定tabll-cell的width一个宽度，一般设成1%就行了。

这样我们就不用在js里去计算了，如果要根据api来按需显示某些cell，可以直接隐藏或显示指定的cell。简单实用。

很遗憾，这个方法在IE上不兼容，不过这中场景大部分应用在移动端，而如今的移动端，几乎可以不用考虑IE。




