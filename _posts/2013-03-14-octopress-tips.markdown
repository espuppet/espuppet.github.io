---
layout: post
title: "Octopress使用归档"
date: 2013-03-14 14:48
comments: true
categories: Archive 
tags: Octopress Archive Tips
---

使用Octopress的几个小技巧和之前遇到的一些配置及使用的问题，这里整理记下来。

主要参考了[Blogging With Plugins](http://octopress.org/docs/blogging/plugins)，[File Binder](https://github.com/aycabta/octopress-file-binder)，[在Octopress中使用Latex](http://yanping.me/cn/blog/2012/03/10/octopress-with-latex/)以及[縮短重新產生文章的時間](http://blog.eddie.com.tw/2011/10/30/speed-up-octopress-post-regeneration/)。

<!-- more -->

##Octopress中图片的插入

换了个主题以后，发现之前的图片显示不了了，然后查了下文档顺便Google了一下。发现以前的链接写错了，而且Octopress自带有[Image Tag](http://octopress.org/docs/plugins/image-tag/)的插件。

原生的方法是，上传图片到`source/images/`下，然后按照Markdown的写法就好了，注意链接的形式是`/images/name`。当然还可以使用image插件写成

    `img [classname] /path/to/image`

还有一个File Binder的第三方插件可以将图片放到`sources/_posts/YYYY-DD-MM-title_imagename.png`(文章位置为`sources/_posts/YYYY-DD-MM-title.markdown`)，插入图片时，应写成

    `img ./imagename.png`

详见[File Binder](https://github.com/aycabta/octopress-file-binder)。

注意：File Binder时不时会导致图片丢失，是因为在deploy之前，如果使用preview的话，会将图片地址转换为localhost:4000开头。所以，如果使用了preview，需要先generate再deploy。

##Octopress在不同机子之间的拷贝

如果你有多个工作机，你可能需要将Octopress从github上拷贝一份。

    git fetch git@github.com:Username/username.github.com source:master

##Octopress主页省略显示文章

开始我检查了一下`_config.yml`中的`excerpt_link`参数，已经配置好了。但是首页依旧全文显示文章。后来发现需要在文章中间插入`<!-- more -->`，这样此标志后的文章就会在首页隐藏，变成`excerpt_link`配置的文字。

##在Octopress中使用Latex

先安装kramdown包

    gem install kramdown

再将下面的代码插入`<head>`和`</head>`标签中间，就OK了（文件路径是`/source/_include/custom/head.html`）。

{% highlight js %}
    <!-- mathjax config similar to math.stackexchange -->
    
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
    tex2jax: {
    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
    processEscapes: true
    }
    });
    </script>
    
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
    tex2jax: {
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
    }
    });
    </script>
    
    <script type="text/x-mathjax-config">
    MathJax.Hub.Queue(function() {
            var all = MathJax.Hub.getAllJax(), i;
            for(i=0; i < all.length; i += 1) {
            all[i].SourceElement().parentNode.className += ' has-jax';
            }
            });
    </script>
    
    <script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>
{% endhighlight %}

##代码高亮

高亮代码使用codeblock即可。

##read_yaml错误

今天很诡异地发现`rake generate`竟然通不过了，然后`rake preview`也没有新的文章了，然后在网上google了方法竟然都没有用。

我的这边提示是`invalid byte sequence in utf-8`，然后看到网上一个网友提示说，查找下文章中的非法字符。反复查找后发现，由于我使用了filebinder，图片文件是和文章放在一起的，然后最近的一个图片的名字格式命名错误，改完后一切OK。

##提高预览文章速度

之前预览文章时，都是先`rake generate`，然后再`rake preview`，需要等好长时间。最后在网上找到了这篇文章[縮短重新產生文章的時間](http://blog.eddie.com.tw/2011/10/30/speed-up-octopress-post-regeneration/)。

当预览某篇文章时`rake isolate[某篇文章]`，这样Octopress就只会生成一篇文章并且将其他文章放到`/source/_stash`里边。当你要发布的时候，要先`rake integrate`将移到`/source/_stash`里的文章移回`/source/_posts`中，再`rake generate`最后再`rake deploy`。


