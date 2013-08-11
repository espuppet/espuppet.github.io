---
title: 记一些零散的配置
author: desc1984
layout: post
categories: Archive
tags: Linux php Tips Nginx
---

昨天装了LNMP，感觉还不错，不过有些地方与原先的Apache不太一样，记录一下。

* 开发环境，我们最喜欢看到127.0.0.1下是一个索引，但是默认Nginx并不是这样。  
 
    在nginx.conf文件中的http字段下添加： 
    
    > autoindex on;//开启自动索引  
    > autoindex\_exact\_size off;//不显示文件详细大小，只显示近似值
* 开发环境，我一般都离不开Xdebug,但是似乎用pecl安装并不成功，只能手工编译。而过程中主要会遇到两个问题:  
 
    - `./configur`e的阶段，系统找不到`php-config`，索引要加一个选项`–-with-php-config=/wp-content/local/php/bin/php-config`;  
     
    - 安装默认并不会在php.ini中添加加载模块，所以要在php.ini中添加一句`zend\_extension=Path/xdebug.so`(PS路径一定要写绝对路径，明明xdebug.so在php.iextension\_dir目录中，但是写相对路径就是不行，不知道为什么……)
* 这个博客刚恢复的时候，由于rewrite没有设置对，导致点击博客其他页面或者后台登录都是404。其实LNMP安装包里默认有Typecho的Rewrite配置，不过不会给根目录配置。  
 
    在Nginx的conf文件夹中找到typecho.conf，将其内容拷贝至nginx.conf文件中server字段下。

昨天想用php写一个自动生成给定大小文件的脚本，但是调试了很多次都没有成功，而且还搞宕机一次……  

查手册才发现filesize这个函数的结果会被缓存，不能动态的获取文件大小（坑爹啊……），导致循环成了死循环。  

后来用fwrite返还值作为循环条件，就没有问题了。
