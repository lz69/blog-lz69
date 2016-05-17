+++
title = "Web前端之JavaScript，DOM，jQuery，AJAX和JSON"
date = "2016-03-29T15:41:05+08:00"
tags = ["Web前端"]
categories = ["Web前端"]
menu = ""
+++

JavaScript是世界上最流行的脚本语言，被设计为相HTML页面增加交互性。
<!--more-->

## JavaScript使用

HTML 中的脚本必须位于 script 标签中。在script标签中可以显示使用
type="text/javascript" 指定使用的脚本语言为javascript，现代浏览器中使用javascript
作为默认的脚本语言。script 标签可以插入 head 和 body 标签中。

#### body 标签中的JavaScript
通常在需要调用某个js函数的时候使用

    <script>
      document.write("<h1>This is a heading</h1>");
    </script>

#### head 标签中的JavaScript
通常在此处引用外部的.js脚本，然后在外部的.js脚本中编写js函数

    //引用外部.js文件
    <script src="myScript.js"></script>

    //myScript.js
    function myFunction()
    {
      document.getElementById("demo").innerHTML="My First JavaScript Function";
    }

## HTML DOM 简介

HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。
HTML DOM 模型被构造为对象的树如下图

![HTML DOM 树](http://7xrnow.com1.z0.glb.clouddn.com/blog_ct_htmltree.gif "HTML DOM 树")

JavaScript脚本可以通过查找到HTML中对应的DOM元素来改变其对应的属性，样式，以及事件反应。

一些常用的 HTML DOM 方法：
* getElementById(id) - 获取带有指定 id 的节点（元素）
* appendChild(node) - 插入新的子节点（元素）
* removeChild(node) - 删除子节点（元素）

一些常用的 HTML DOM 属性：
* innerHTML - 节点（元素）的文本值
* parentNode - 节点（元素）的父节点
* childNodes - 节点（元素）的子节点
* attributes - 节点（元素）的属性节点

## jQuery 简介

jQuery是一个JavaScript库，用以简化JavaScript编程。

jQuery 库包含以下特性：
* HTML 元素选取
* HTML 元素操作
* CSS 操作
* HTML 事件函数
* JavaScript 特效和动画
* HTML DOM 遍历和修改

jQuery简单语法

    $(this).hide() //隐藏当前的 HTML 元素。
    $("#test").hide() //隐藏 id="test" 的元素。
    $("p").hide() //隐藏所有 <p> 元素。
    $(".test").hide() //隐藏所有 class="test" 的元素。

## AJAX 简介

AJAX既Asynchronous JavaScript and XML（异步的 JavaScript 和 XML），是一种使用现有
标准的新方法，可以在不重新加载整个页面的情况下，与服务器进行数据交换。

XHR(XMLHttpRequest)是AJAX的基础。使用过程如下

创建XHR对象

    xmlhttp=new XMLHttpRequest();

向服务器发送请求

    //method：请求的类型；GET 或 POST
    //url：文件在服务器上的位置
    //async：true（异步）或 false（同步）
    xmlhttp.open(method,url,async);
    //string：仅用于 POST 请求
    xmlhttp.send(string);

获取服务器响应

    //获得字符串形式的响应数据。
    responseText
    //获得 XML 形式的响应数据。
    responseXML

当请求发送到服务器后，可以基于不同的响应，给予不同的执行任务。

onreadystatechange	存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。

readyState存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
* 0: 请求未初始化
* 1: 服务器连接已建立
* 2: 请求已接收
* 3: 请求处理中
* 4: 请求已完成，且响应已就绪

status
* 200: "OK"
* 404: 未找到页面

    xmlhttp.onreadystatechange=function()
    {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
      {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
      }
    }

## JSON简介
JSON 指的是 JavaScript 对象表示法（JavaScript Object Notation）,是一种轻量级的，独立于
语言的文本数据交换格式。

JSON 语法是 JavaScript 对象表示法语法的子集。
* 数据在名称/值对中
* 数据由逗号分隔
* 花括号保存对象
* 方括号保存数组

实例
    {
    "employees": [
        { "firstName":"John" , "lastName":"Doe" },
        { "firstName":"Anna" , "lastName":"Smith" },
        { "firstName":"Peter" , "lastName":"Jones" }
      ]
    }
