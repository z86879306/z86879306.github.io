---
title: axios发送post请求数据后台无法接收问题
date: 2018-11-27 14:00:05
tags: axios
---
最近尝试使用**iview-admin** 来做前后端分离开发
使用**axios**代替**ajax**请求


当参数是JSON对象时，默认的Content-Type是application/json。
此时后台无法获取所传递的参数
>在axios使用Post发送数据时，默认是直接把json放到请求体中提交到后端的，而后端获取数据的方式有两种，一种是@RequestParam（通过字符串中解析出参数）,另一种是@ResponseBody（从请求体中取参数），很显然，我们的后端用了第一种方式。

解决如下: 
```
import Qs from 'qs'
```
```
export const deleteAudioType = (id) => {
  let data = {
    id: id
  }
  return axios.request({
    url: 'api/audio/deleteType',
    data: Qs.stringify(data),
    method: 'post'
  })
}
```
使用qs 库对数据进行转换 ，此时结果如下：
![发送数据请求](https://upload-images.jianshu.io/upload_images/5122776-c73e62f25ba31f7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

传递的为表单数据 contetn-type 为aplication/x-www-form-urlencoded

问题解决
