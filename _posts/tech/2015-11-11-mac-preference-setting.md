---
layout: post
category: tech
tags: tech
keywords: finder terminal
description: finder terminal
title: mac下finder和terminal的切换
---

## terminal --> finder

在MAC下，有时我们在终端里操作的文件目录想要快速的用finder打开当前目录。
这时如果文件目录很深的话，直接用finder去是很痛苦的，甚至还会找不到。
当人你也许会轻轻告诉我你的秘方，说先在终端输入
```
pwd
```

查看绝对文件路径后再用finder一层一层翻。
这样当然可以。
但是还有一个能秒开的命令
```
open .
```

直接就是用finder打开当前目录
顺便 open --help 了一下，几个值得一记的参数

* -a 是指定APP名称打开文件
	eg:
	```
	open -a Safari http://www.baidu.com
	```

用safari打开百度

* -e 用edittext打开文件
	eg:
	```
	open -e test.txt
	```

装逼足矣.

## finder --> terminal

MAC默认是不能在finder中直接打开terminal的，但是我们（特别是开发者）往往有这样的需求。
MAC这么强大，这种刚需肯定考虑到了的，所以通过系统偏好设置就可以做到。
打开系统偏好设置>键盘>服务
选择这两项：
![img](/images/mac_setting.png)



