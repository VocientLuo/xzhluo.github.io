---
layout: post
category: tech
tags: tech
keywords: nodejs des加密 zip
description: nodejs的des加密，zip压缩
title: nodejs的des加密和zip压缩
---

## des加密

众所周知，我们Java里面对des加密很通用，也有很规范的库，用起来很方便。

但是在js的世界里，就比较麻烦，比如应用后台的API是java写的，且API通过des加密，如果前后端分离，或者处于完全分离的两个服务，就比较麻烦。

这里麻烦的地方有两点：

* 后端API不能动；

* 前端js无法实现des加密解密。

现在的应用都是前后端分离，因此这种场景比较常见了。

那怎么解决呢？

其实方法还是有的。我们应用前后端分离，但前端的代码终究是要放在服务器上的，所以，我们可以做一个代理层，不管我们的服务器上跑的是java还是其他语言，只要把这个加密解密的工作放在后台来做，就会迎刃而解。

这里看一种如果后端是nodejs的解决方法。

nodejs的des加解密库有很多线程的库，因此也会造成一个选择困难，到底用哪一套。

这里推荐一个跟java的加解密能吻合的库，crypto。

它是用npm来管理的，所以只要用```npm install crypto```安装即可。

加解密的使用过程如下：

* 加解密的封装

```
var cryptos = require("crypto");
var mkey = "G15-NIPR";
var ivKey = [0x12, 0x34, 0x56, 0x78, 0x90, 0xAB, 0xCD, 0xEF];
var util = {
    algorithm:{ ecb:'des-ecb',cbc:'des-cbc' },
    //des base64加密
    encrypt:function(plaintext){
        var key = new Buffer(mkey);
        var iv = new Buffer(ivKey);
        var cipher = cryptos.createCipheriv(this.algorithm.cbc, key, iv);
        cipher.setAutoPadding(true);
        var ciph = cipher.update(plaintext, 'utf8', 'base64');
        ciph += cipher.final('base64');
        return ciph;
    },
    decrypt:function(plaintext){
        var key = new Buffer(mkey);
        var iv = new Buffer(ivKey);
        var decipher = cryptos.createDecipheriv(this.algorithm.cbc, key, iv);
        decipher.setAutoPadding(true);
        var text = decipher.update(plaintext, 'base64','utf8');
        text += decipher.final("utf8");
        return text;
    }
}
module.exports = util;
```

这里des加密后最终输出的是base64编码后的结果

同理解密也是。

* 封装后的使用

```
var crypt = require('./crypto-util');
var data = crypt.encrypt(string); //对字符串进行des加密，解密使用decrypt
```

## zip压缩

这里不是前端页面的zip压缩，是指接口数据压缩。

这是有现成的压缩库的，也是有很多，nodejs有自带的zip库。

这里推荐一个库,```gzip-buffer```，这个压缩库是能更java的gzip压缩对上号的。

提供的方法也很简单：

```
gzip.gzip(buffer);//buffer进行gzip压缩
gzip.gunzip(buffer);//gzip解压缩
```




