---
layout: post
title: "C语言中的变长参数"
date: 2013-05-25 17:48
comments: true
categories: Program
tags: Program C
---

最近做了一份C语言的习题，接触到了C语言中的变长参数（函数的参数个数可变），就像printf等函数。

# 实现

C中可变参数通过`va_start`,`va_end`和`va_arg`三个宏以及一个类型`va_list`实现。

{% highlight c %}
void va_start(va_list varlist, param N);
    
void va_end(va_list varlist);
    
type va_arg(va_list varlist, type);

{% endhighlight %}
# 例子

{% highlight c %}
#include <stdio.h>
#include <stdarg.h>

int sum_va(int, ...);

int main() {
    int cal;
    cal = sum_va(6,2,3,4,1,1,1);
    printf("%d",cal);
    return 0;
}

int sum_va(int num,...) {
    int i=0,sum=0;
    va_list varlist;//定义参数列表

    va_start(varlist, num);//初始化参数列表

    for(i=1;i<=num;i++)
        sum += va_arg(varlist,int);//获取参数

    va_end(varlist);//关闭参数列表

    return sum;
}
{% endhighlight %}
