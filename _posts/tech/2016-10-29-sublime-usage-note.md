---
layout: post
category: tech
tags: tech
keywords: sublime usage
description: sublime使用心得
title: sublime使用笔记
---

## 1.使用package console 管理插件

### 第一步
 
选择sublime菜单栏的View > show console 	快捷键：ctrl+` (mac)

### 第二步

把下面的代码拷贝到弹出的命令行窗口

sublime text3

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

sublime text2

```
import urllib2,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

拷贝后回车， sublime左下角会出现'Installing package...'的提示

安装后会有提示窗口。

下面我们就可以通过快捷键```cmd+shift+p```很方便的打开命令行输入窗口去安装插件。

## 2.安装主题

推荐两个比较漂亮的主题：soda,spacegray

### 第一步

使用快捷键```cmd+shift+p```打开命令行，输入pci,pci是package console install,sublime会模糊匹配到

![img](/images/pci.png)

回车后sublime的左下角会先出现loading repo...的提示，这时是在加载插件仓库。完成会出现插件输入框。

我们可以在输入框里输入想要的插件，这里我们以soda为例，在输入框里输入soda

### 第二步

![img](/images/soda.png)

找到 theme soda后回车

左下角会出现安装soda的提示。安装好后可能需要重启sublime才能生效。

## 3.安装AdvancedNewFile

这是一个快速创建文件的插件。能够快速建立文件到指定目录。

在安装之前，我们可能会通过```cmd+n```创建一个文件，事实证明这个方法的保存文件太麻烦

而安装之后，我们可以很方便创建文件到指定目录下，即使这个目录不存在，也会自动创建目录。

### 第一步

安装方法跟上面安装主题是一样的。不再多说

### 第二步

我们使用时通过```cmd+alt+n```即可输入指定文件或者文件目录下的文件即可

![img](/images/advancednewfile.png)

## 4.emmet插件

这是一个强大的插件，应该是sublime玩家必备装备。

安装过程省略。我们看一下这个插件的功能：

* Expand Abbreviation

   快速编写html代码，语法很简单。

   比如我们要写一段这样的html：

```
<div id="page">
<div id="title"></div>
<div id="content">
<h1>hello,world</h1>
<p></p>
</div>
<div id="foo"></div>
</div>   
```

   要这样写很费劲，但是这个使用这个插件你只需这样写：

   ```
   #page>#header+(#content>h1{hello world}+p)+#foot
   ```

   对于程序员来说，这真是爽到没朋友。

   我们使用时需要通过快捷键：```ctrl+e```激活

* Match Tag Pair Outward, Inward
	
	通过快捷键```cmd+d```来选择整个标签内容，包括标签，可以叠加

	通过快捷键```cmd+shift+d```来选择整个标签内容，不包括标签，可以叠加


* Go to Matching Pair
	
	光标迅速移动到标签的开头和结尾，快捷键：```cmd+t```

* Wrap With Abbreviation

	在光标处添加  Expand Abbreviation	 格式的html。快捷键：```cmd+shift+a```

* Go to Edit Point
	
	光标在标签里面切换 快捷键：```ctrl+alt+←```或者```ctrl+alt+→```

* Select Item
	
	选择节点(单词，标签，内容),快捷键：```cmd+shift+,```或者```cmd+shift+.```

* Toggle Comment

	注释整个标签，快捷键：```cmd+/```

* Remove Tag
	
	移除标签，不包括子标签，快捷键：```cmd+k```

* Update Image Size

	给图片标签添加尺寸信息，可用于img标签和css样式里，快捷键：```cmd+shift+u```

* Evaluate Math Expression

	快速做数学运算，快捷键：```cmd+shift+y```

* Reflect CSS Value

	css快速兼容，同一个属性的-webkit,-moz等属性能快速同步，快捷键：```cmd+b```

* Encode/Decode Image to data:URL

	图片快速转码成url，快捷键：```cmd+shift+i```


## 总结

之前一直用atom开发前端，虽然atom也很强大，但是总觉得有些地方不方便，比如打开大文件会卡死，这个貌似还没法解决。

然后看到很多同事在用sublime，而且也推荐使用，因此想熟练一下。

可以感觉到，sublime比atome还是优越一些，从插件上，性能上。atom要打开大的文件夹也会卡。sublime感觉上好多了。

而且atom上有的插件，sublime上基本都有。

sublime使用package console管理插件，插件官网是：[https://packagecontrol.io/browse](https://packagecontrol.io/browse)

很丰富，而且很有意思。







