---
title: springboot拦截器跨域配置
date: 2018-12-07 14:37:02
tags:
- 跨域
---

由于前后端分离的部署情况，后台设置了允许跨域请求

在测试环境中发现，被拦截器拦截的请求**response**的**header**并没有设置跨域。

这是个没注意到坑，补上代码

```
//拦截器跨域请求设置
                response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE");
                response.setHeader("Access-Control-Max-Age", "3600");
                response.setHeader("Access-Control-Allow-Credentials", "true");
                response.setHeader("Access-Control-Allow-Headers", "x-requested-with");
                response.setHeader("Access-Control-Allow-Origin", request.getHeader("Origin"));
```

