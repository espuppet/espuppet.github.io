---
title: XDebug与XHProf的一些对比
author: admin
layout: post
categories: Program Web
tags: php Program Web
---

功能上：  
XDebug：  
变量显示、堆栈跟踪、函数追踪、代码覆盖率分析、剖析PHP脚本、远程调试  
XHProf:  
平面统计（调用次数，inclusive/exclusive消耗时间，内存消耗以及CPU时间）、分层统计（Parent及Child调用次数及时间）、差别统计、调用图、内存消耗

上手难度：  
XDebug:  
参数较多，具有一定的上手难度  
XHProf:  
仅有一对开关函数，以及几个参量，上手难度较低

性能：  
从功能上就可以看出，XDebug针对的是开发环境，帮助开发者更为有效的理顺思路、调用顺序以及找到Bug；而XHProf针对的是生产环境，追踪产生大量消耗CPU,或者内存的代码。  
而且，XHProf更有轻量级的 xhprof\_sample\_enable()和xhprof\_sample\_disable()这样一种运行方式。  
虽然没有经过实际检验，但是我觉得XHProf无疑效率更高，因为它针对的是生产环境。

官方支持：  
XDebug最近的一个版本2.1.2是2011-07-28释出的，而上一个版本2.1.1是在2011-03-28释出的。开发的很活跃，应该支持也比较好吧。  
XHProf最近的一个版本0.9.2beta则是2009-06-01释出的。可能，版本较为稳定不需要怎么更新。
