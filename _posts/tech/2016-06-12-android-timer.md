---
layout: post
category: tech
tags: tech
keywords: android timer
description: 
title: android中Timer的使用
---

安卓中的Timer是个定时器，它的黄金搭档是TimerTask。

Timer的作用是在指定的时间执行某项任务，而TimerTask就是这个任务的载体。

eg:

```
new Timer().schedule(new TimerTask() {
            @Override
            public void run() {
                // do something
            }
        },delay,period);
```

delay参数是表示要延迟多长时间执行这个task。

period参数可选，表示隔多长时间循环执行，没有这个参数表示单次执行。

Timer一般一个Activity(Service)里只需要一个，在使用前注意要清理一下内存，免得多个同样的task在Timer中执行。


