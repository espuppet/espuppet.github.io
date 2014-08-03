---
layout: post
title: "初识SaltStack"
date: 2014-07-22 22:50
categories: DevOps
tags: DevOps SaltStack
---

博客又是好久没有更新了，期间起起伏伏，还是从象牙塔里走出来了。最近在做一些DevOps相关的调研，这里总结一下。

SaltStack算是一个比较新的工具，但是其受到广泛的好评。这里有两篇比较好的介绍--[集群管理工具](http://www.cnblogs.com/alexyang8/p/3445333.html)和[salt的主要功能及使用](https://holbrook.github.io/2013/06/25/salt_usage.html)。官方也有两篇介绍文字也算全面--[Introduction to Salt](http://docs.saltstack.com/en/latest/topics/index.html)和[SaltStack Walk-throug](http://docs.saltstack.com/en/latest/topics/tutorials/walkthrough.html)

表明上看起来SaltStack的用法十分简单，但是深入之后还是有一些地方相对比较晦涩，这里整理一下中间遇到的问题以及相关的参考资料。

- PATH问题   
在使用cmd.run时，在minion端实际执行命令的service的PATH与其他用户是不同的，所以如果执行与PATH变量相关的命令，最好指定SHELL和ENV。详细的参数介绍，请参考[这里](http://docs.saltstack.com/en/latest/ref/states/all/salt.states.cmd.html#salt.states.cmd.run)。问题相关，参考[PATH being overwritten](https://github.com/saltstack/salt/issues/6785)。

- 分组   
指定分组时，如果有多个minion需要使用参数L，比如"L@minion1,minion2"，参考[Compound matchers](http://docs.saltstack.com/en/latest/topics/targeting/compound.html)当时在这里，坑了好久。。。
