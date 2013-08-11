---
title: Ubuntu下Empathy登录QQ
author: admin
layout: post
categories: Archive
tags: QQ Archive Ubuntu 
---

Ubuntu里的Empathy本来是支持QQ的，但是非常可惜登录不了……  
于是Google之，找到解决办法：  
打开终端，添加源

> sudo add-apt-repository ppa:lainme/libqq

然后更新之

> sudo apt-get update

然后安装之

> sudo apt-get install libqq-pidgin

然后，没有然后了，你的Empathy可以登录QQ了~

有没有发现Empathy的声音提示非常鸡肋，基本听不见！  
我们自己来动手改，虽然比较麻烦……  
系统里用的声音都在这里：

> /wp-content/share/sound

注意到这里有ubuntu文件夹，没错，这里就是声音选项卡里声音主题里的Ubuntu。如果把ubuntu/stereo里的message-new-instant.oga替换掉，就可以了。  
但是这个ogg/oga格式真是令人蛋疼，木事，我们有Gnac,链接在这里  
[http://gnac.sourceforge.net/][1]  
可以通过这种方式来安装

 [1]: http://gnac.sourceforge.net/ "gnac"

> $ sudo add-apt-repository ppa:gnac-team/ppa  
> $ sudo apt-get update  
> $ sudo apt-get install gna

PS:别报报警音量给静音了，那样你永远都听不到声音……
