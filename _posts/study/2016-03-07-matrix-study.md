---
layout: post
category: study
tags: study
keywords: 矩阵
description: 矩阵的运算
title: 矩阵的运算
---

今天搞懂了矩阵的运算，加，减，乘。加减都很容易理解，乘法有点难理解，但是跟线性方程式放在一起，就比较容易理解。

* 矩阵的加法

两个矩阵相加，是每个矩阵的每个对应的位置上的数字相加。

* 矩阵的减法

两个矩阵相减，是前一个矩阵的每个位置上的数字减去第二个矩阵的对应位置上的数字的结果

* 矩阵的乘法

两个矩阵相乘，结果矩阵的第m行第n列的数值是第一个矩阵的第m行的每个值与第二个矩阵的第n列的对应位置上的每个值相乘的结果再相加后的值。

这在线性方程式中很有用，比如线性方程式中有两个方程式：

```
3x+7y=10
5x+6y=14
```

就可以用矩阵表示成：

```
| 3  7 |   | x |   | 10 |
| 5  6 |   | y |   | 14 |
```


参考资料：

[http://www.ruanyifeng.com/blog/2015/09/matrix-multiplication.html](http://www.ruanyifeng.com/blog/2015/09/matrix-multiplication.html)


