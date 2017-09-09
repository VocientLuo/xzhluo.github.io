---
layout: post
category: tech
tags: tech
keywords: shell git 多仓库备份
description: shell+git多项目多仓库备份
title: shell+git多项目多仓库备份
---

这个需求还是比较常见的，尤其是国内，如果我们的仓库放在国外网站上，免不了会段誉一阳指式的时灵时不灵。这时我们往往考虑到的是把这些repo备份到国内网站。

这里就以我自己的github上的repo备份到oschina上为例。

## 备份要求

* 多个仓库同时备份

* 完整备份，包括分支，commit

* 定期同步

要做到这几个要求，要手动备份几乎是不可能的。

那怎么办呢？

看了下oschina上的repo管理，发现了一个功能

![img](/images/sync.png)

oschina上的repo可以填一个强行同步另一个远程仓库的功能，感觉看到了一丝希望。

说实话，这个功能还没试过，但要满足上面的备份要求，估计也难以做到。

自己撸袖子吧。

先整理一下思路：

![img](/images/think.png)

思路大概是这样，以本地仓库为跳板，把github上的仓库拉下来，包括分支，然后在本地仓库加入oschina的仓库地址，然后往oschina上推。

这整个过程用shell来完成，下面展示具体的示例，

我在github上有一个backtest的repo，有两次提交，两个分支：

![img](/images/commit.png)

![img](/images/remote.png)

先在oschina上建好准备备份的仓库，以便执行shell时一次性就能推上去：

![img](/images/oschina_repo.png)

这是我在oschina上建的一个空仓库。

接下来就是写shell脚本了

```
 #! /bin/bash
  2
  3 # project name
  4 project=backtest
  5
  6 # github repo url
  7 github_url=https://github.com/vicent900527/
  8 # oschina repo url
  9 oschina_url=https://git.oschina.net/vicentor/
 10
 11 # clone github repo
 12 git clone "${github_url}${project}".git ${project}
 13 # inter project dir
 14 cd "${project}"
 15
 16 # add oschina repo url into git config remote, name oschina
 17 git remote add oschina "${oschina_url}${project}".git
 18
 19 # get all branches
 20 branches=$(git branch -r)
 21
 22 # erdogic branches and push it
 23 for line in ${branches}
 24 {
 25     #截取出分支名称，并去掉HEAD,->这样的分支，这是不存在的，
 26     branch=${line#*/}
 27     if [ "${branch}" != "HEAD" ] && [ "${branch}" != "->" ];
 28     then
 29         git checkout "${branch}"
 30         git pull
 30         git pull
 31         git push oschina --all
 32     fi
 33 }
```

在看运行结果：

![img](/images/run_result.png)

再看看oschina上的仓库：

![img](/images/oschina_result.png)

嗯，就酱。差不多就可以了。

额，虽然做到了多分支，保持了commit，但是多仓库同时倒腾过去的呢？

嗯，这个就把shell里的project变成数组，再从克隆那里开始循环project数组，在循环里做下面的工作就可以了。

定期同步呢？定期同步就更简单了，可以自行百度crontab。




