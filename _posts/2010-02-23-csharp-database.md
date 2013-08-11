---
title: 'C#操作数据库'
author: admin
layout: post
categories: Program
tags: C# Program
---

最近在写一个C#打印程序，其中要用到数据库的一些操作，现在记下来，备忘。以Mysql为例(Mysql要下载一个dll，声明using MySql.Data.MySqlClient;)

    {% highlight c# %}
    String connectionString = “server=127.0.0.1;user id=root; password=123456; database=test; pooling=false;charset=utf8″;  
    MySqlConnection connect = new MySqlConnection(connectionString);
    
    connect.Open();  
    MySqlCommand command = connect.CreateCommand();  
    command.CommandText = “Select * from test where type = 0″;  
    MySqlDataReader Reader = command.ExecuteReader();
    
    while (Reader.Read())  
    {  
    Console.WriteLine(Reader["index"]);  
    }  
    connect.Close();  
    Console.Read();
    {% endhighlight %}
