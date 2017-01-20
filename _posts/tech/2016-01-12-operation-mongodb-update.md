---
layout: post
category: tech
tags: tech
keywords: mongodb 更新字段
description: mongodb更新数据表
title: MongoDB更新数据表
---

MongoDB中的collection的字段值可能是个json对象，这是如果直接更新这个字段就会可能把对象中原有的一些值覆盖掉，
因此我们可以在终端这样做：
```
db.pagemodels.find({_id:ObjectId("569479c8281d61706acda196")}).forEach(function(d){
  if(d.fild1.fild2){
    d.fild1.fild1.fild3= "value";
    db.pagemodels.save(d);
  }
})
```

先把这条数据查出来，然后就可以像操作JSON数据一样修改JSON的具体的某条值，修改后再保存这条数据，很妥。