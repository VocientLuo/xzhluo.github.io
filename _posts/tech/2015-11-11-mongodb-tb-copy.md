---
layout: post
category: tech
tags: tech
keywords: mongodb
description: MongoDB数据表批量拷贝
title: MongoDB数据批量拷贝
---
把当前数据库中的tb_a中的数据拷贝到db_b数据库中的tb_a中
```
db.tb_a.find().forEach(function(d){db.getSiblingDB('db_b')['tb_a'].insert(d);})
```

解释：
把tb_a中的数据全部取出并逐行插入到db_b数据库中的tb_a中。
```
db.getSiblingDb：
```

官网的解释是：a database object

所以 
```
db.getSiblingDB('db_b')['tb_a'] 
```

是指db_b数据库中的tb_a表
所以相当于 
```
db_b.tb_a.insert(d) ; 
```

对tb_a执行插入操作

思考：
这里除了一些mongodb用到的固定方法，其余的都是js语法，所以这里在的function也可以对行进行想要的修改操作。

mongodb官方文档[点这里](http://docs.mongoing.com/manual-zh)
