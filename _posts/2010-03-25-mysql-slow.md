---
title: 关于Mysql远程连接速度慢
author: admin
layout: post
categories: Program
tags: Mysql Tips
---

最近用另一台机子远程连接Mysql，发现速度奇慢无比。  
Google后，解决问题。

在my.ini文件里添加

> [mysqld]  
> skip-name-resolve  
> skip-grant-tables

skip-name-resolve：禁用DNS解析，连接速度会快很多。不过，这样的话就不能在MySQL的授权表中使用主机名了而只能用ip格式。

–skip-grant-tables：系统将对任何用户的访问不做任何访问控制，但可以用 mysqladmin flush-privileges或mysqladmin reload来开启访问控制;默认情况是show databases语句对所有用户开放，

如果mysql服务器没有开远程帐户，就在my.ini里面加上skip-grant-tables
