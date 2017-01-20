---
layout: post
category: tech
tags: tech
keywords: node express
description: express代理转发请求
title: express代理转发请求
---

在浏览器中，我们使用js发送ajax请求非当前域名的服务器时，是有跨域的问题的。
也就是说，如果我们在js里请求第三方服务器是会被浏览器拦截，导致请求失败。
这个问题有两种解决方案：

* 请求的第三方服务器设置response的header，对响应头不要限制请求方法。

* 通过请求自己的服务器，服务器代理这个请求转发出去。

第一种通常我们可能没有去操作的权限。
通常我们会使用第二种，因为我们对自己的服务器有充分的权限。
如果是express的后台，我们需要注意几个点，才能顺利的完成整个代理流程。
先看看代码：

```
http = require 'http'
url = require 'url'
_ = require 'underscore'
queryString = require 'querystring'

module.exports = (options) ->

  return (req, res, next) ->
    # 查找符合规则的代理配置
    k = _.chain(options).keys().find (k) ->
      req.url.match new RegExp(k)
    .value()
    unless k
      next()
    else
      server_config = options[k]
      #get the right url from routing
      if k != req.url
        # find in the route's definition
        if k.indexOf('*') > 0
          regex = new RegExp(k.replace('*', '(.+)'));
          path = regex.exec(req.url);
          server_config = server_config.replace('*', path.splice(1)) if path
      console.log "proxy #{req.url} to remote service #{server_config}"
      req_opt = url.parse server_config
      # TODO handle error event to avoid exit with error because of wrong proxy
      # console.log "#{JSON.stringify(req_opt)}"
      console.log req.body
      req_options = {
        hostname: req_opt.hostname
        port: req_opt.port
        path: req_opt.path
        method: req.method
        headers: {}
      }
      request = http.request req_options
      , (response) ->
        res.writeHead response.statusCode, response.headers
        response.pipe(res)
        response.on 'data', (data) ->
          console.log "代理转发[服务器]响应: #{response.statusCode}, #{data.toString()}"

        response.on 'error', (e) ->
          console.log 'problem with response: ' + e.message
      #catch exception
      request.on 'error', (e) ->
        console.log "error happend when write to the background server, #{e}"
      request.write(queryString.stringify(req.body))
      request.end()
      req.on 'error', (e) ->
        console.log 'problem with request: ' + e.message

      req.on 'end', ->
        request.end()
```

这是coffee代码，主要逻辑就是：拦截请求——>匹配需要代理的请求——>组装代理请求http.request——>设置request的参数——>发送请求——>得到的响应结果返回.
需要注意两个点：

* 代理请求的options的headers不能使用前请求的req.headers，这样会导致直接返回404，原因没详查。因此这里就填了{}

* 代理转发的写入时需要使用到body-parser这个插件否则读取req.body是空的。这个在配置express的时候使用即可。

