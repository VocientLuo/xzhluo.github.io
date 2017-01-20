---
layout: post
category: tech
tags: tech
keywords: android studio style
description: android studio的使用心得
title: android studio 使用心得
---

android studio简称安卓开发神器。

其中有一些功能实在是溜到不行，这里记下几个。

### 自动生成style
---

秉着代码复用的原则，我们的layout文件会尽可能的使用style，这样其他View的样式就可以使用同一个style，这个在静态行式菜单布局会用的特别多。

如果是在eclipse中，我们要去styles文件里新添一个样式，把属性逐一加到items里面去。这样也很麻烦。

但在android studio中，我们可以很快搞定。

只要在layout文件中，选中你写好的样式，右键>Refactor>Extract>Style然后填写样式名称即可。

![img](/images/as_auto_build_style.png)

这个功能简直炫到没朋友。

### 从github上加载开源包
---

在eclipse中，我们加载jar包是要下载jar包，然后放到libs下，作为引用。

但在android studio中，就省事多了，只要一行代码就能搞定。

我们在build.gradle中添加一条 compile即可。

比如我们通常用到的xUtils工具，可以这样：

```
dependencies {
    ...
    compile 'org.xutils:xutils:3.3.34'
}
```

然后sync即可。

### 对bean文件中的变量添加get/set方法
---

这个功能在eclipse中也有，但确实是个非常爽的功能。

在android studio中，只要 ```ctrl+n``` 就能添加，也可以单独选择get或者set方法：

![img](/images/as_get_set.png)

### 快速打开已有安卓工程
---

很多安卓开发者会经常查看一些开源工程的代码，会从github或者其他地方获取到这样的安卓工程，然后用android studio打开来看。

但是通常会遇到android studio中的gradle和要导入的工程的gradle版本不对应。这样android studio就会半天都打不开这个工程。

这是android studio一个非常烦的问题。这问题在国外或许没有，但是天朝没办法，只能稍微绕一下。

gradle版本不对我们可以把版本换成android studio中已有的gradle，这要改两个地方：

* 1 找到要打开的工程里的build.gradle文件，用文本编辑器打开。

找到：

```
dependencies {
        classpath 'com.android.tools.build:gradle:2.1.2'
}
```

这行代码，把gradle版本替换成你本地的gradle版本，如果不知道怎么找，可以用android studio创建一个新工程或者已经存在的工程，然后打开build.gradle文件，把这行复制过来。

* 2 找到要打开的工程的gradle文件夹。

![img](/images/as_gradle_version.png)

把wrapper文件夹下的这两个文件用第一步的方法替换掉。

完成这两步，再用android studio去打开这个工程，就能快速的打开了。

原理很简单，就是把要打开的工程的gradle版本换成本地已有的gradle版本。






