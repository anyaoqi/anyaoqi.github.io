---
title: react跨域安装Http-proxy-middleware报错
date: 2022-10-16 20:46:01
tags:
categoryes: 
  - 踩坑之路
---

## react跨域安装Http-proxy-middleware报错：proxy is not a function


查看了http-proxy-middleware的官方文档，发现最新的1.0.0版本已经对模块的引用作了明确的要求

* 0.x.x版本的引用方式

```javascript
const proxy = require('http-proxy-middleware');
```

* 1.0.0版本的引用方式

```javascript
const { createProxyMiddleware } = require('http-proxy-middleware');
```

