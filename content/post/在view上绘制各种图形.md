+++
title = "在View上绘制各种图形"
date = "2016-04-06T14:35:33+08:00"
##tags = ["Android"]
##categories = ["Android"]
menu = ""
+++

在View上绘制图形主要是，继承View，然后重写它的onDraw(Canvas canvas)方法,在其中Canvas
上利用Paint来进行绘画
<!--more-->

## Demo运行效果

![Demo运行效果](http://7xrnow.com1.z0.glb.clouddn.com/blog_view_ondraw.gif)

## Canvas

Canvas是画布的意思，负责承载我们要进行绘制的各种图形，主要有如下的一些绘制图形接口

* drawArc 绘制弧
* drawBitmap 绘制位图
* drawCircle 绘制圆形
* drawLine 绘制线
* drawOval 绘制椭圆
* drawPath 绘制路径
* drawPoint 绘制一个点
* drawPoints 绘制多个点
* drawRect 绘制矩形
* drawRoundRect 绘制圆角矩形
* drawText 绘制字符串
* drawTextOnPath 沿着路径绘制字符串


## Paint

Paint是颜料的意思，主要用来设置绘图的风格，主要有如下的一些设置接口

* setARGP/setColor 设置颜色
* setAlpha 设置透明度
* setAntiAlias 设置是否有抗锯齿
* setShader 设置画笔的填充效果
* setShadowLayer 设置阴影
* setStyle 设置画笔的风格
* setStrokeWidth 设置空心边框的宽度
* setTextSize 设置绘制文本时文字的大小

## Path
Path是指路径的意思，你可以使用圆形，矩形，弧，或者几个点的连线来生成一条Path。

## 坐标体系

从左上角开始，向右为x轴正轴方向，向下为y轴正轴方向。在onDraw中坐标，大小的单位都是px。

## 绘制图形
在View中通过重写onDraw()绘制图形的方法很简单。

首先重写onDraw方法，以绘制圆形举例。

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        //新建一个Paint对象
        Paint paint = new Paint();
        paint.setAntiAlias(true);
        paint.setColor(getResources().getColor(android.R.color.holo_green_dark));
        //在Canvas上绘制圆形
        canvas.drawCircle(150, 150, 100, paint);
    }

然后在xml文件中就可以使用我们的CircleView了

    <com.lz69.viewondraw_demo.view.CircleView
        android:layout_width="match_parent"
        android:layout_height="100dp"/>

## Demo链接
https://github.com/lz69/ViewOnDrawShape-Demo
