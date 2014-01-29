---
title: Cake环境配置说明
author: admin
layout: post
categories: Program Web
tags: Program php
---

1.Apache的配置文件http.conf:

>   
> Options FollowSymLinks  
> AllowOverride all  
> Order Deny,Allow  
> Deny from all  
> Allow from 127.0.0.1  
>  

加载模块：

> LoadModule rewrite\_module modules/mod\_rewrite.so

2.PHP配置文件php.ini（修改后重启才生效！）

> Include_path = //网站目录

3.权限配置：  
cake需要有对/cake/app文件写入的权限。
