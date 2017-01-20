---
layout: post
category: tech
tags: tech
keywords: Atom 个性化
description: Atom个性化设置
title: Atom个性化，Snipets
---

Atom的spinets是自定义代码块的快捷键配置文件，我们可以根据自己的编码习惯，在该文件里配置一些模块化的代码块。
比如基于backbone中的一些语法块，看看我做的配置：

```
'.source.js':
  #1. define common class
  'common class':
    'prefix': 'def'
    'body': 'define([\'$1\'], function($2){\n\t$3\n});'
  #2. define view extend baseView
  'V etd BV':
    'prefix': 'defbv'
    'body': 'define([\'./BaseView\'], function(BaseView){\n\treturn BaseView.extend({\n\t\t$1\n\t});\n});'
  #3. define view extend PageView
  'V etd PV':
    'prefix': 'defpv'
    'body': 'define([\'./PageView\'], function(PageView){\n\treturn PageView.extend({\n\t\ttype:\'$1\',\n\t\tinitialize: function(){},\n\t\tconfigure:function(options){$2},\n\t\trender:function(){\n\t\t\tPageView.prototype.render.apply(this,arguments);\n\t\t\treturn this;\n\t\t},\n\t});\n});'
  #4. define function is so easy
  'function(){}':
    'prefix': ': '
    'body': ': function($1){\n\t$2\n},'
```

这是一个coffee语法的cson文件，
coffee是通过缩进做语法控制。下面对上面的代码做下解释：

```
'.source.js' 
# 申明下面的代码适用哪种文件，这里表示适用后缀为.js的文件。
	'common class':
	# 输入 def 时提示 common class
		'prefix': 'def'
		# 输入 def 简码
		'body': 'define([\'$1\'], function($2){\n\t$3\n});'
		# 输入 def 后回车时会补充完整的代码块 \n表示换行，\t表示一个tab，$1表示回车后光标出现的地方，$2表示按tab键后光标出现的地方，$3跟$2一样。
```

这是一个完整的snipets,下面的可以看出是循环这个语法。

### 应用
打开Atom的菜单栏，选择 'Open your Spinets'
在弹出的cson文件里直接做写入这些即可。
保存后发现，只要键入prefix的内容，回车即可出现一整块代码。
我定义的第四个，能很好的解决我在编码时总是带入java的编写习惯，因为java定义方法是方法名后面直接带括号加参数再加大括号的形式，因此犯过几次错，有了这个后，只要输入 : 回车，就能把function写出来。
看看效果：
1.
![img](/images/function_prefix.png)
2.
![img](/images/function_result.png)



