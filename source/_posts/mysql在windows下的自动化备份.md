---
title: mysql在windows下的自动化备份
date: 2018-11-24 10:49:55
tags:
- 备份
- 自动化
categories:
- mysql
---
今天在公交车上看见公众号的一篇推文讲述的是一个数据库误操作的事件。
在线上版本的程序如果发生这样的事情将是一个很大的灾难，可能会造成巨大的损失。想到此处，发觉自己对数据的备份的意识还是太缺失,但是手工备份过于麻烦，且容易忘记。
作为一个懒人是不允许这样的事情发生的，程序员应该让计算机帮我们干事情不是吗=。=
># [Windows下为MySQL做定时备份](https://www.cnblogs.com/frankielf0921/p/5933127.html)
参考了网上的方案，决定使用 **[mysqldump](http://www.111cn.net/tags.php/mysqldump/)备份成sql文件**

废话不多说 直接上代码

基于公司现使用的服务器是**windows**，虽然我也不知道为什么是windows(很尴尬）

新建一个 **db_backup.bat** 批处理文件，利用windows自带的任务计划程序做一个定时执行的脚本
```
@echo off
set "Ymd=%date:~,4%%date:~5,2%%date:~8,2%"
E:/mysql/mysql-5.7.15-winx64/bin/mysqldump --opt -u root --password=123456 party-build > D:/db_backup/bbs_%Ymd%.sql
@echo on
```
说明：此方法可以不用关闭数据库，并且可以按每一天的时间来名称备份文件。
通过%date:\~5,2%来组合得出当前日期，组合的效果为yyyymmdd,date命令得到的日期格式默认为yyyy-mm-dd(如果不是此格式可以通过pause命令来暂停命令行窗口看通过%date:~,20%得到的当前计算机日期格式)，所以通过%date:~5,2%即可得到日期中的第五个字符开始的两个字符，例如今天为2009-02-05,通过%date:~5,2%则可以得到02。（日期的字符串的下标是从0开始的）

可以先bat 脚本后面增加 pasue 来检查执行结果。任务计划程序的步骤很简单，不再过多的陈述。

结果：
![执行结果.png](https://upload-images.jianshu.io/upload_images/5122776-b5b8dfd532e38dc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

完美~
