---
layout: post
title: "Vim配置"
date: 2012-11-25 13:53 
comments: true
categories: Vim
tags: Vim
---

本篇文章介绍VIM如何配置和一些优秀的VIM插件。

VIM的使用因人而异，每个人有每个人的使用习惯，所以配置文件还需要各位自己参考别人的配置文件，最终写出适合自己的配置文件。否则，即使配置文件再强大，也发挥不了作用。

网上流传一份[史上最强VIM配置文件(html高亮版)](http://www.amix.dk/vim/vimrc.html)，这里有[纯txt版](http://www.amix.dk/vim/vimrc.txt)。我的配置文件也是从中修改过来的，具有很好的参考价值。

当然，你还可以参考[这里](https://github.com/humiaozuzu/dot-vimrc)，里面涵盖了不少插件的配置，我的自动补全就是从这里借鉴的。

<!-- more -->

这里重点讲几点：

##  字体及主题推荐

推荐的编程字体为DejaVu Sans Mono，推荐的自带colorscheme koehler，当然可以去下载网上的其他颜色方案，自己看着爽就好了。

##  关于Windows乱码的解决

此处参考VIMIM给出的解决方法：

{% highlight vim %}
set encoding=utf-8
if g:iswindows==1
set termencoding=GBK
else
    set termencoding=utf-8
    endif
    set fileencoding=utf-8
    set fileencodingileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1
    set langmenu=zh_CN.utf-8
    source $VIMRUNTIME/delmenu.vim
    source $VIMRUNTIME/menu.vim
    language messages zh_cn.utf-8
{% endhighlight %}

##  底部状态栏的修改

上面的配置文件的状态栏只能显示所在行，我们可以添加上所在列。

{% highlight vim %}
    set statusline=\ %{HasPaste()}%F%m%r%h\ %w\ \ CWD:\ %r%{getcwd()}%h\ \ \ POS:\ %l,%v
{% endhighlight %}

##  VIM插件</strong>

* 插件管理：  
    这里推荐使用Vundle(https://github.com/gmarik/vundle)来管理VIM插件，非常方便与实用，只需要在配置文件写一行就并执行命令，就可以实现插件的自动安装与卸载。
    - 首先，你需要安装git(此部分略去)。
    - 然后按照Vundle的说明执行就好了。
    在命令行下执行：
        {% highlight bash %}
        git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
        {% endhighlight %}
    然后按照说明在配置文件中写入下面部分(当然插件可以自己选了)：
    
{% highlight vim %}
set nocompatible               " be iMproved
filetype off                   " required!

set rtp+=~/.vim/bundle/vundle/
call vundle#rc()

" let Vundle manage Vundle
" required! 
Bundle 'gmarik/vundle'

" My Bundles here:
"
" original repos on github
Bundle 'tpope/vim-fugitive'
Bundle 'Lokaltog/vim-easymotion'
Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
Bundle 'tpope/vim-rails.git'
" vim-scripts repos
Bundle 'L9'
Bundle 'FuzzyFinder'
" non github repos
Bundle 'git://git.wincent.com/command-t.git'
" ...

filetype plugin indent on     " required!
{% endhighlight %}

    然后在VIM中执行:BundleInstall，它就会自动帮你安装插件了。</li>

* NerDTree:  
    虽然说VIM自带文件管理的功能，但是比起NerDTree还是不够方便。推荐的NerDTree配置如下，快捷键映射为F7：

{% highlight vim %}
let NERDTreeChDirMode=2
let NERDTreeWinSize=30
let NERDTreeWinPos = "right"
let NERDTreeIgnore=['\.vim$', '\~$', '\.pyc$', '\.swp$']
let NERDTreeSortOrder=['^__\.py$', '\/$', '*', '\.swp$',  '\~$']
nmap <F7> :NERDTreeToggle<CR>
{% endhighlight %}

##  自动补全：

想必使用VIM码代码的人最需要的功能就是这个了吧，我使用的是neocomplcache+snipmate+supertab，借鉴了上面提到的配置文件，配置如下：

{% highlight vim %}
" neocomplcache

" Use neocomplcache.
let g:neocomplcache_enable_at_startup = 1
" Use smartcase.
let g:neocomplcache_enable_smart_case = 1
" Use underbar completion.
let g:neocomplcache_enable_underbar_completion = 1
let g:neocomplcache_disable_auto_complete=1
let g:neocomplcache_min_syntax_length=3
set completeopt-=preview

" SuperTab

let g:SuperTabRetainCompletiontype = 2
let g:supertabdefaultcompletionType = "<C-X><C-U>"
{% endhighlight %}
