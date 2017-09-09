---
layout: post
category: tech
tags: tech
keywords: jekyll 安装
description: jekyll安装失败的问题
title: jekyll安装不成功
---

jekyll是在github上建博客的一个工具（功能不止于此），基于ruby开发，在国内安装时通常会报各种各样的错误。

主要原因在于ruby使用在国内无法访问国外的安装包存放站点。

比如在执行gem install jekyll时会报这样的错：

```
ERROR:  Could not find a valid gem 'jekyll' (>= 0), here is why:
          Unable to download data from http://ruby.taobao.org - bad response Not Found 404 (http://ruby.taobao.org/latest_specs.4.8.gz)
```

这是ruby的一个国内镜像现在无法访问了.

我们看一下当前的资源地址：gem sources -l

可以看到```http://ruby.taobao.org```这个就在里面

这个是不能用了，需要更新。

改成```https://gems.ruby-china.org/```就可以了

操作如下：

```
gem sources --remove http://ruby.taobao.org

gem source -a https://gems.ruby-china.org/

```

然后执行

```
sudo install jekyll
```

即可





