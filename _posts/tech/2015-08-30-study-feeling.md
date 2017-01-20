---
layout: post
category: tech
tags: tech
keywords: swift
description: 学习swift
title: Swift入门学习
---

这段日子知识的摄入量可以用一个词概括，多而杂。

* javascript
* swift
* c++

javascript，是在左项目时用到，由于之前有过功底，所以不是太难，一些简单的数据处理还是能搞定。
c++是考试课程，就强迫性的看看了。

swift,也是手里有玩iOS的工具，兴趣性的看了 [慕课网](http://www.imooc.com)上的一些视频，在java里呆久了一开始接触这个还真是不太适应。

从语法上完全是颠覆性的不同，一开始看觉得有点像javascript。

因为swift命名变量是用var关键字。

比如：
<pre><code>var length = 100</code></pre>
length就是一个初始值为100的变量，这是不是跟js很像？
还有一个跟js很像的地方就是代码行尾不一定要分号，这就看上去更像js了。
还有一个相似的地方就是函数的申明和使用，swift里有一个闭包的概念。

什么叫闭包？
我的理解就是：函数的形式参数可以是一个完整的方法。就像js里的function a(function(){})；这种类似。
不过再往下看基本就跟js拉开距离了。
swift是对象行语言，上面的 var length = 100只是一个小细节而已。

还有另外一个让java程序员非常难以接受的是swift中变量类型的申明是在变量名后面的。
比如：
<pre><code>
	func sayHello(name : String)->String
	{
    	let result = "hello ,"+(name)+"!";
    	return result;
	}
</code></pre>
这个函数里，函数的返回值类型是String，并有一个名位name的String类型的形参。
但是这个写法，如果你也是玩java的，你肯定接受不了这样毁三观的变态方式。
这点太奇怪了，想不明白开发语言的为啥要这样折腾，跟c,c++,java...这些保持风格一致有那么难吗？

真正玩了一下xcode这个工具就知道了，之前开发iOS是用Object-c，而OC的风格就是这样的，这样奇葩的。
新出来的swift肯定要考虑兼容OC的，所以就只好这样了。

这就像我们的交通一样，世界交通是车辆靠左行驶，当年蒋一声令下所有车辆靠右行驶。

不得不佩服蒋的创意，给后来中国的经济带来了多大的推动力就可想而知了，从此所有的进口车辆都得二次改装后才能上路，方向盘得从右边改到左边去。（其实就是一个人犯错全国人民买单。）

历史故事点到即止。学到的swift的语法还没记录完。

学习一段之后就会发现里面还是有很多有意思的地方。
比如，通常普通的函数申明里函数的形参可以理解成传入的实际参数的一个副本，函数体力对该参数的写操作是不会改变外面的实参值的。
<pre><code>
var number = 10;
func changeNum(var n : Int)->Int
{
    n = n+10;
    return n;
}
println(changeNum(number));
println(number);
</code></pre>
这段代码最后打印的20,10
也就是说，函数changeNum操作一次变量number后没有实际去改变number的值的，但我们会有这样的需求。
swift有一个关键字inout可以描述函数形参的，加上它之后就会改变number的值。
<pre>
	<code>
var number = 10;
func changeNum(inout n : Int)->Int
{
    n = n+10;
    return n;
}
println(changeNum(&number));
println(number);		
	</code>
</pre>
这里的打印就是20,20了。
如果加了这个inout关键字后，在调用changeNum里就需要给传入的变量加上&字符了。
其实很好理解，这就相当于指针的概念，这个函数就是传递了指针，函数体就是改变指针的指向的内存存储值。
其实更像C++里引用的概念，C++中引用是对指针的一个封装，在变量名前用&表示，引用的好处就是对内存起到保护的作用。
因为C++里指针是能通过整形强制转换成来的，因为指针就是一个内存编号，这就会有一个数据安全的问题。而引用就避免了这个问题，

嗯，觉得还是挺有意思的。还有很多很奇葩的东西，后续继续分享。