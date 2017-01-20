---
layout: post
category: tech
tags: tech
keywords: nodejs 微信登录
description: nodejs应用实现微信登录
title: nodejs应用实现微信登录
---

web应用使用微信登录的方式有多种。
比如：

* 扫码登录

* 微信应用里授权登录

最终目的无非就一个：微信授权给web应用获取用户信息，实现简易登录。

技术层面，实现流程也基本一致。

可以分为几步：

* 1 第一步：用户同意授权，获取code
* 2 第二步：通过code换取网页授权access_token
* 3 第三步：刷新access_token（如果需要）
* 4 第四步：拉取用户信息(需scope为 snsapi_userinfo)

步骤不难，下面我们来看nodejs的应用怎么做。

这个案例是nodejs的express的应用，coffee代码。

* 第一步 应用定向到微信登录地址

```
app.get "/wx_login.html",(req,res) ->
  # 准备微信授权地址
  wxUrl = "https://open.weixin.qq.com/connect/oauth2/authorize?" 
  appid = "appid=" + wx_appid
  # 回调地址
  redirect_uri = "redirect_uri=http%3A%2F%2F" + wx_redirect_uri +"%2Fwx_token.html"
  response_type = "response_type=code"
  scope = "scope=snsapi_userinfo"
  wx_state = "state=cfmall#wechat_redirect"
  # 拼装授权地址完成
  authUrl = wxUrl + appid + "&" + redirect_uri + "&" + response_type + "&" + scope + "&" + wx_state
  # 重定向请求，转向微信授权页面，用户授权后会进入上面的毁掉地址wx_token.html并把微信的code传过来
  res.redirect authUrl
```

这一步做的工作就是获取code。

* 第二步 获取token

```
app.get "/wx_token.html",(req,res) ->
  # 获取微信回传的code
  code = req.query.code
  if !code
  	# 出错处理，做登录失败处理
    res.redirect 'index.html'
    return;
  # 组装获取token的url
  code = "code=" + code
  tokenUrl = "https://api.weixin.qq.com/sns/oauth2/access_token?"
  appid = "appid=" + wx_appid
  secret = "secret=" + wx_secret
  grant_type= "grant_type=authorization_code"
  access_token_url = tokenUrl + "&" + appid + "&" + secret + "&" + code + "&" + grant_type
  # 组装完成，开始请求
  http.get access_token_url
  , (response) ->
    response.on 'data', (data) ->
      if data
      	# 拿到token后开始获取用户信息
        userInfoUrl = "https://api.weixin.qq.com/sns/userinfo?access_token="
        openId = "&openid="
        lang = "&lang=zh_CN"
        data = JSON.parse data.toString()
        infoUrl = userInfoUrl + data.access_token + openId + data.openid + lang
        http.get infoUrl
        , (infoRes) ->
          infoRes.on 'data', (wxData) ->
            # 获取用户信息 wxData
            app_obj.wxInfo = wxData
            # do something
          infoRes.on 'error', (e) ->
            # 错误处理 do something
      else
        # 错误处理 do something
    response.on 'error', (e) ->
      # 错误处理 do something
```

that's all.

是的，就是这么简单。

