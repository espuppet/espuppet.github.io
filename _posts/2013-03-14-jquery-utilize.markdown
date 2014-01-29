---
layout: post
title: "jQuery使用相关"
date: 2013-03-14 17:41
comments: true
categories: Program Web
tags: Web jQuery Program
---

最近接触到一些Javascript，感觉Ajax比较强大，比PHP这样的服务器端脚本灵活许多。由于自己本身不会JS，也就只能边搜索边用，好在有jQuery，用起来真的比较方便。

使用到的插件有时间选择插件[jQuery-UI-datePicker](http://jqueryui.com/datepicker/)和[jQuery-UI-TimePicker-addon](http://trentrichardson.com/examples/timepicker/)以及分页插件[dataTables](http://www.datatables.net/)。

<!-- more -->

##jQuery-UI-datePicker和jQuery-UI-TimePicker

TimePicker实际是datePicker的一个插件，需要嵌入datePicke中使用。由于项目中有限制时间选择区间的需求，可以借助Timepicker中的`minDateTime`和`maxDateTime`参数实现。

{% highlight js %}
var current = new Date();
var temp = current.getDay() + 7;
var maxDate = new Date();
limit.setDate(temp);
$('#targetID').datetimepicker({
    showSecond: true,
    timeFormat: 'HH:mm:ss',
    stepHour: 2,
    stepMinute: 10,
    stepSecond: 10,
    minDateTime: current,
    maxDateTime: maxDate,
});
{% endhighlight %}

##dataTables

dataTables的数据来源有四种：DOM,Javascript数组，Ajax源以及服务器端数据。由于项目中的数据比较多，所以选择了最后一种。具体的可以参考[官方文档](http://www.datatables.net/examples/data_sources/server_side.html)。

dataTables的初始化：

{% highlight js %}
var oTable=$('#jq_tablepage').dataTable({
        "bSort": false,
        "bPaginate": true,
        "bJQueryUI": false,
        "sPaginationType": "full_numbers",
        "sAjaxSource": "../examples_support/server_processing.php"
        "oLanguage": {
        "sUrl": "./js/datatable.language"}
        });
{% endhighlight %}

Ajax向服务器请求数据是传入的参数有：显示起始数`iDisplayStart`，显示条目数`iDisplayLength`，排序列数目`iSortingClos`，排序列`iSortingClo_1`以及搜索条件`sSearch`。

其中，服务器端需要返回的数据格式如下。

{% highlight php %}
$output = array(
        "sEcho" => intval($_GET['sEcho']),
        "iTotalRecords" => $iTotal,
        "iTotalDisplayRecords" => $iFilteredTotal,
        "aaData" => array()
        );
{% endhighlight %}

sEcho由前端AJAX请求产生，可以在`$_GET`中获得，`$iTotal`为查询条目总数，`$iFilteredTotal`为加上过滤条件后的条目总数，`aaData`为实际数据，格式为无Index的Json格式。
