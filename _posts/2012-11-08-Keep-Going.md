---
layout: post
title: "Keep Going"
date: 2012-11-08 14:59
comments: true
categories: Archive
tags: Archive Tips
---

##新的开始，新的故事

考虑了蛮久的，也尝试了好久，最后还是决定将博客迁到这里。

Typecho是个不错的博客程序，轻量、快速、便捷。但是好的系统自然需要一个好的生态,很遗憾，Typecho的生态并不丰富。而与Jekyll相比，Typecho的轻量又没有了优势。

毋庸置疑，当今博客的主流仍然是Wordpress。但是Wordpress的臃肿与缓慢，又被许多人所诟病。虽然前阵子看到了[Ghost:博客工具的“简单主意"](http://www.ifanr.com/189450),但是项目仍未成型，前景未卜，喜欢Wordpress的朋友倒是可以去关注下。

既然搬迁到了Jekyll就把配置过程记录一下，其实过程是有些曲折的。

<!-- more -->
    
    
##Jekyll入门

我一开始是参考[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)这篇文章来配置的，但是需要注意的是，gh-pages是用来生成项目介绍网站的，所以文章中是生成了gh-pages分支。而如果你想要配置域名为userid.github.com这样的个人博客，需要新建一个名为userid.github.com的项目，上传文件到此项目中即可，不需要生成gh-pages分支。

而有关Jekyll的配置，就需要去参考[官方文档](https://github.com/mojombo/jekyll/wiki)了。这里倒是有一份[BlackCube的主题代码](https://github.com/pizn/blogTheme/tree/master/BlackCubeTheme)可以参考下。
    
    
##Git入门

学习Git最好就是看文档了，推荐两份：[看日记学git](http://roclinux.cn/?p=914),[git community book中文版](http://gitbook.liuhui998.com/)
    
    
##Jekyll本地调试

其实当初原本是想用Octpress的，但是Octpress要求Ruby 1.9.3，当时鼓捣了好久没配好，- -！。后来想想算了，就用了Jekyll。当时配了十多次，硬是没有配成功，最后终于找到了篇靠谱的文章配好了，就是这篇[如何快速正确的安装 Ruby, Rails 运行环境](http://ruby-china.org/wiki/install_ruby_guide) (还是官方Wiki靠谱。。。)。其实Jekyll可以说是原生支持目录的，因为在[Plugins](https://github.com/mojombo/jekyll/wiki/Plugins)的说明中就提及了。具体的实现可以参考这里，[为Jekyll博客添加category分类](https://github.com/mojombo/jekyll/wiki/Plugins)


