---
title: 'C# 中ListView的基本使用'
author: admin
layout: post
categories: Program
tags: C#
---

添加列(也可在Column属性中添加)  
`this.listView1.Columns.Add(title);`  
添加子条目  
{% highlight c# %}
while(Reader.Read())
{
ListViewItem Li = new ListViewItem();
Li.Text = Reader["No"].ToString();
Li.SubItems.Add(Reader["Time"].ToString());
Li.SubItems.Add(Reader["XM"].ToString());
listView1.Items.Add(Li);
}  
{% endhighlight %}
删除子条目(用Visible属性是为了不影响速度)  
{% highlight c# %}
this.listView1.Visible = false;
            this.listView1.Items.Clear();
            this.listView1.Visible = true;`
{% endhighlight %}
