---
layout: post
category: tech
tags: tech
keywords: phantom
description: npm phantom
title: npm install phantom
---

in our project,you maybe have this error when you run server:
```
Error: Cannot find module 'phantom'
at Function.Module._resolveFilename (module.js:336:15)
at Function.Module._load (module.js:278:25)
at Module.require (module.js:365:17)
at require (module.js:384:17)
```

you can do this:
```
npm install phantom --save
```