---
title: 关于使用thumbnails 图片压缩png格式问题
date: 2018-12-11 09:22:46
tags:
categories:
- 开发问题
---

##thumbnail压缩

之前的开发没有对上传的图片进行压缩，考虑到用户体验，加载的速度快慢决定在服务端加上压缩图片的处理

如果使用阿里的oss系统也是能达到这样的效果

```
	File file = new File("C:/Users/Administrator/Desktop/img/if_apple_2003193.png");
	InputStream inputStream = new FileInputStream(file);
	Thumbnails.of(inputStream)
			.scale(1f)
			.outputQuality(0.8f)
			.toFile("C:/Users/Administrator/Pictures/111.jpg");
```
api使用非常简单，稍微有点基础就能使用

这里记录一下所遇到的问题，如果压缩的源文件是使用QQ截图获得的png文件，压缩获得的文件大小反而是大于源文件的文件大小的，且图片的质量是低于源QQ截图文件，
具体原因猜测是QQ已经对截图的文件做过压缩处理,处理的效果还是高于我所使用的thumbnail 在保持图片高质量的情况下，还能尽量的压缩图片的大小。


