---
layout: post
category: tech
tags: tech
keywords: js
description: js学习
title: JavaScript中形式参数的理解
---
JavaScript中的形参跟其他语言不一样，比如Java语言，
我们定义方法是这样

```
static void Main(){
	sayHello("hello world");
}
public void sayHello(String str){
	System.out.println(str);
}
```

这里的sayHello方法里使用了形参str，String类型，并在Main方法里调用。结果会打印hello world。
这是Java的参数使用。
相比之下，JavaScript就要灵活的多，它除了能像上面这么用，还能像下面这样：

```
function sayHello(){
	console.log(arguments[0]);
}
sayHello("hello world");
```

这是因为，JavaScript与其他语言不同，它的方法里的参数，是放在arguments对象里，所以在方法体里可以直接通过arguments对象拿到参数；像上面这样写也不会报错。
当然，这样写也没错的：

```
function sayHello(str){
	console.log(str);
}
sayHello("hello world");
```

在JavaScript中形参的申明只是为了更方便直观的取到参数，因此JavaScript不会关心形参是否有定义，或者定义了几个。
当然，这里的str和上面的arguments[0]是指向同一个内存值的，因此修改str，arguments[0]的值也会跟着变。

