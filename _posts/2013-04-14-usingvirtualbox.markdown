---
layout: post
title: "Windows下使用VirtualBox归档"
date: 2013-04-14 11:40
comments: true
categories: Archive
tags: Tips VirtualBox
---

使用Linux的时间不短了，重启Windows进入Linux抑或重启Linux进入Windows实在是让人纠结。还是决定使用VirtualBox了，即可以享受Linux的开发环境，还可以使用Windows下丰富的软件。

这里记录一些使用中遇到的问题，方便以后查找：Debian下安装VirtualBox Guest Additions，修正VirtualBox共享文件权限以及通过Dropbox同步项目代码。

<!-- more -->

## Debian下安装VirtualBox Guest Additions

VirtualBox的无缝模式做得真的很棒，但是需要安装Guest Additions，当然这并不是什么难事。

只需要将GuestAddition光盘（在安装目录下）挂载到系统中，执行脚本VBoxLinuxAdditions.run即可。

但是需要安装一些依赖：

    apt-get install gcc make linux-headers-$(uname -r)

## VirtualBox下修正共享文件权限

使用VirutalBox默认的自动挂载时，虽然可以挂载到/media下，但是所有者是root，使用时需要来回切换权限。

通过手动挂载，修改/etc/fstab文件，可以修正权限

     FolderName /media/foldername/ vobxsf rw,gid=,uid=,auto 0 0

第一个参数为VirtualBox中共享文件夹名，第二个从参数为挂载点，第三个是vbox共享文件夹特有的文件格式。

## 通过Dropbox同步项目代码

这个我主要参考这篇[Git教學：Git的遠端操作及利用Dropbox建立Server進行協同開發(Windows)](http://www.mrmu.com.tw/2011/05/06/git-using-dropbox-as-server/)文章。简单总结一下：

在Dropbox下新建一个文件夹，然后初始化git:

    git init --bare

添加bare参数后，这个仓库只保存git历史提交的版本信息，不容易出现冲突。所以建议远端repo使用bare初始化。

在自己项目中，添加远程源：

    git remote add origin Dropbox的目录/Project

然后照常push,pull即可。
