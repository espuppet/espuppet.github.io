---
layout: post
title: "动态对象创建"
date: 2013-08-29 21:44
comments: true
categories: Program C++
tags: Program C++
---

《C++编程思想》中的第六章初始化与清除和第十三章动态对象创建的内容比较接近，在这里一起总结。

<Effective C++>中的第二章与这部分内容也相近，也放在这里了。

## 初始化与清除

* 应该在尽可能靠近变量的使用点处定义变量，并在定义时就初始化
* 以指针传递数组时，会丢失数组信息
* 可以这样计算数组大小：`sizeof(c)/sizeof(*c)`

## 动态对象创建

![动态对象创建](/assets/2013-08-29-construct-destruct.png)

## Constructor,Destructor,and Assignment

* Know what functions C++ silently writes and calls  
  编译器默认生成类的默认构造函数，拷贝构造函数，拷贝赋值运算符和析构函数  
* Explicitly disallow the use of compiler-generated functions you do not want  
  声明相应成员函数为private，且不实现可以禁止编译器自动生产此函数。可以使用一个Uncopyable基类来实现此目的。  
* Declare destructors virtual in polymorphic base classes  
  多态/基类应声明虚析构函数,并同时提供对虚函数的定义。如果一个类没有任何虚函数，就不应该有虚析构函数。  
  除了基类和使用多态的类外，不应该使用虚析构函数  
* Prevent exceptions from leaving destructors  
  析构函数不应该出现异常。如果调用的析构函数抛出异常，那么析构函数应该捕获这个异常并swallow这个异常，或者终止程序  
  如果客户需要捕获异常并作出反映，那么异常应该在非析构函数中抛出。  
* Never call virtual functions during construction or destruction  
  此时调用虚函数只会调用基类版本和本地版本，而不会调用子类中的对应函数。  
* Have assignment operators return a reference to `*this`  
* Handle assignment to self in operator=  
  确保`operator=`在对自己进行赋值时well-beahved.可以使用的技术有：比较源对象和目标对象的地址，仔细安排语句的顺序和copy-and-swap  
  确保当函数作用与两个或更多个对象时well-beahved  
* Copy all parts of an object  
  拷贝函数应当拷贝一个对象的数据成员和所有基类部分  
  不要实现在一个拷贝函数中使用另外一个拷贝函数，把公共部分放到第三个函数中。

