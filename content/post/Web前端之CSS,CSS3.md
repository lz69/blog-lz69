+++
title = "Web前端之CSS,CSS3"
date = "2016-03-25T16:08:11+08:00"
tags = ["Web前端"]
categories = ["技术相关"]
menu = ""

+++

HTML 标签原本被设计为用于定义文档内容,而CSS用于定义文档显示的样式。

<!--more-->

## 1. CSS 简介

CSS 全称为Cascading Style Sheets，既层叠样式表。通过将样式保存在一个.css文件中，极大
得提高了我们改变网站布局和外观的工作效率。

## 2. CSS 语法

### 2.1 基本格式

    selector1, selector2 {
      property1: value1;
      property2: value2;
    }

selector通常为需要改变样式的HTML元素，property为需要改变的HTML元素的属性，value为
需要改变的HTML元素的值。

### 2.2 派生选择器

    li strong {
      font-style: italic;
      font-weight: normal;
    }

改变 li 标签中的 strong 标签内容的样式

### 2.3 id 选择器

    #red p {
      color:red;
    }
    <p id="red">这个段落是红色。</p>

改变id为red的p(可省略)标签内容的样式，规定同一HTML文档中同一id只能给予一个HTML元素。

### 2.4 类选择器

    .red p {
      color:red;
    }
    p.red {
      color:red;
    }
    <p class="red">这个段落是红色。</p>

改变class为red的p(可省略)标签内容的样式。

### 2.5 属性选择器

    [property]
    {
      color:red;
    }
    <p property="">这个段落是红色。</p>

改变设置了property属性标签内容的样式，也可以指定property属性中包含的特定字符串才改变样式

## 3. CSS 样式

在CSS中提供了很多的属性可以用来改变标签内容的样式，比如改变背景，文本，字体，链接，列表，表格，轮廓等等

## 4. CSS 框模型

元素框(element)的最内部分是实际的内容，它有自己的宽(width)和高(height)，直接包围
元素框(element)的是内边距(padding)。内边距呈现了元素框(element)的背景。内边距的边缘
是边框(border)。边框(border)以外是外边距，外边距(margin)默认是透明的，因此不会遮挡其后的任何元素。

## 5 CSS 定位

### 5.1 CSS 相对定位(relative)

如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，
让这个元素“相对于”它的起点进行移动。无论是否进行移动，元素仍然占据原来的空间，
因此，移动元素会导致它覆盖其它框。

### 5.2 CSS 绝对定位(absolute)

设置为绝对定位的元素框从文档流完全删除，绝对定位使元素的位置与文档流无关，因此不占据空间。
绝对定位的元素的位置相对于最近的已定位祖先元素，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块。

### 5.3 CSS 浮动定位

浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。

## 6. CSS3 简介

CSS3 是最新的 CSS 标准，其中包含了大量的新特性，比如背景和边框文本效果，2D/3D 转换，动画，多列布局，用户界面等等。
