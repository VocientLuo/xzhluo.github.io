---
layout: post
category: tech
tags: tech
keywords: react
description: react学习
title: mac下react环境搭建
---

* #### 建立工作环境：####
	在终端建立工作空间，并初始化

	``` 
		mkdir react
		cd react
		bower init
	```

    完成后会在目录下生成一个bower.json文件。
* #### 安装react ####
    这时可以把react安装了：

    ```
    bower install react --save
    ```

    ![image](/images/create.png)

* #### 安装依赖 ####

	```
	npm install -g babel
	```

	babel是为引用JSX库使用的。
很简单，我们的react工作环境就建立起来了。

接下来我们写个简单的例子。
把刚才的目录用atom打开，创建一个index.html文件。
index.html的文件内容：

```
<html>
  <head>
    <meta charset="utf-8">
    <title>React Todo</title>
    <!-- 引入react -->
    <script type="text/javascript" src="./bower_components/react/react.js" charset='utf-8'></script>
  </head>
  <body>
    <div id='container'></div>
  </body>
</html>
```

这时我们可以打开index.html，是一个空白的网页。
接下来在根目录下建立src文件夹，并在src下新建test.js，并新增如下代码：

```
var Hello = React.createClass({
  render: function(){
    return <h1> hello world </h1>;
  }
});
React.render(<Hello /> , document.getElementById('container'));
```

编译src目录：

```
 babel src --watch --out-dir build
```
这里是把src目录下的文件输出到build目录下。
完成后在在index.html中引入test.js文件，注意，这里的路劲不是src目录下的test.js，而是build目录下的test.js，原因是react运行时会自动把编译后的js放入build目录下去。

```
<script type="text/javascript" src="./build/todo.js"></script>
```

好，到这里，我们可以在终端运行react了。
这时刷新我们的浏览器，就能看到hello world了。

![image](/images/react_result.jpeg)



