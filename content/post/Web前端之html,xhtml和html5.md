+++
title = "Web前端之HTML,XHTML和HTML5"
date = "2016-03-24T14:03:11+08:00"
tags = ["Web前端"]
categories = ["Web前端"]
menu = ""
+++

最近在复习web前端相关的一些知识点，在本篇总结一些HTML,XHTML和HTML5之间的关系和主要知识点
其中XHTML更像是对你写HTML时，建议的一些做法，以便HTML可以兼容更新的浏览器，而HTML5更像
是原HTML的扩展包，它可以让你实现很多原HTML所实现不了的一些事情。

<!--more-->

## 1. HTML

### 1.1 HTML简介

HTML的全拼是Hyper Text Markup Language,既超文本标记语言，通过一系列的标签来描述网页，
通过使用h1，p，table这样的标签告诉浏览器这是标题,这是段落,这是表格之类的信息。

### 1.2 HTML中的基本组成

    <!DOCTYPE html>
    <html>
    <head>
      <title>标题<title>
      <base href="http://www.leonzou.com/" />
      <link rel="stylesheet" type="text/css" href="mystyle.css" />
      <meta name="keywords" content="HTML, XHTML, HTML5" />
      <script type="text/javascript" src="http://leonzou.com/js"></script>
      <link rel="stylesheet" type="text/css" href="mystyle.css" />
    </head>
      <body>
      </body>
    </html>

#### 1.2.1 <!DOCTYPE>声明

<!DOCTYPE>不是HTML中的标签，它用来告诉浏览器html是用什么版本写的，如：

    <!DOCTYPE html>

说明该文档基于html5。

#### 1.2.2 <head>元素

 head 元素是所有头部元素的容器。以下标签都可以添加到 head 部分：

 * title : 定义文档的标题。
 * base : 为页面上的所有链接规定默认地址或默认目标。
 * link : 定义文档与外部资源之间的关系。
 * meta : 提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。
 * script : 用于定义客户端脚本，比如 JavaScript
 * style : 用于为 HTML 文档定义样式信息

### 1.2.3 <body>元素

 body 元素是html文档的主题部分，主要用来展示内容，下面包含大部分用来展示页面的标签，
比如 p , h1 , table , form 等。

## 2. XHTML

### 2.1 XHTML简介

XHTML 指的是可扩展超文本标记语言，是一种必须正确标记且格式良好的标记语言。它更像是限定
HTML中一些不规范的语法的规则。

### 2.2 XHTML语法规则

 * XHTML 元素必须正确嵌套
 * XHTML 元素必须始终关闭
 * XHTML 元素必须小写
 * XHTML 文档必须有一个根元素

## 3. HTML5

### 3.1 HTML5简介

  HTML5更像是HTML的一个扩展包，只不过这个扩展包成为了新的HTML标准。

### 3.2 HTML5新特性

 * 支持对控件进行拖放
 * SVG图形的支持
 * 用于绘画的 canvas 元素
 * 支持地理定位
 * 用于媒介回放的 video 和 audio 元素
 * 用于本地存储的localStorage和sessionStorage
 * 通过创建 cache manifest 文件，对Web应用程序进行缓存
 * 支持在后台运行脚本的Web Worker
 * 允许网页获得来自服务器的更新
 * 新的特殊内容元素，比如 article、footer、header、nav、section
 * 新的表单控件，比如 calendar、date、time、email、url、search
 等等
