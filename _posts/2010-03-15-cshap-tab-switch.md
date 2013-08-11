---
title: 'C#中TabControl切换触发事件'
author: admin
layout: post
categories: Program
tags: C# Program
---

今天要找一个方法用于处理点击某个Tab触发的事件，却发现TabControl控件貌似没有内置这样的事件。  
无奈google，找到一个解决问题的方法(用SelectedIndexChanged事件)：

{% highlight c#%}
switch (this.tabControl1.SelectedIndex)
{
    case 0:
        &ldquo;Tab0 was chosen&rdquo;
        break;
    case 1:"Tab1 was chosen"
           break;
    case 2:
           &ldquo;Tab2 was chosen&rdquo;
           break;
}
{% endhighlight %}
