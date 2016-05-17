+++
title = "Android适配相关"
date = "2016-04-06T14:35:33+08:00"
##tags = ["Android"]
##categories = ["Android"]
menu = ""
+++

包括多国家地区文本适配，
<!--more-->

## 多国家地区文本适配

#### 创建多个values文件夹和string.xml文件

把android studio切换到project项目结构。在app/src/main/res路径下新建
values-en文件夹（同理可以创建其他国家地区对应的文件夹），在里面新建
string.xml文件。系统则会根据当前的语言环境，选择对应的string.xml文件
进行加载。目录结构如下

    res/
      values/
        strings.xml
      values-en/
        strings.xml

相对应的/values/strings.xml

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
      <string name="app_name">安卓适配-示例</string>
      <string name="hello_world">你好 世界！</string>
    </resources>

想对应的/values-en/strings.xml

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
      <string name="app_name">AndroidAdaptive-Demo</string>
      <string name="hello_world">Hello World!</string>
    </resources>

#### 如何使用strings.xml文件

在代码中可以这样

    String hello = getResources().getString(R.string.hello_world);
    textView.setText(R.string.hello_world);

在xml布局中可以这样

    android:text="@string/hello_world"

系统则会根据当前的语言环境，选择对应的string.xml文件进行加载。

## 不同屏幕的适配

要适配不同的屏幕，主要关注屏幕的两个属性，一个是屏幕尺寸（size）,一个是屏幕像素密度（density）

#### 适配不同尺寸

对不同尺寸的屏幕进行适配主要是建立多个不同的layout-<screen_size>-<land>文件夹,相关目录结构如下

    res/
       layout/              # 默认的 (竖屏)
           main.xml
       layout-land/         # 横屏
           main.xml
       layout-large/        # large (竖屏)
           main.xml
       layout-large-land/   # large 横屏
           main.xml

 #### 适配不同的密度

 在不同屏幕密度下，要想图片有相同的显示效果，则需要建立不同的drawable-<dpi>或者mipmap-<dpi>文件夹,现在在
 android studio下新建工程，可以看到对应的启动图标的目录结构,对应的分辨率，以及倍数关系如下

    res/
      mipmap-hdpi/
          ic_launcher.png   72*72   1.5
      mipmap-mdpi/
          ic_launcher.png   48*48   1(基本线)
      mipmap-xhdpi/
          ic_launcher.png   96*96   2
      mipmap-xxhdpi/
          ic_launcher.png   144*144 3
      mipmap-xxxhdpi/
          ic_launcher.png   192*192 4

## 不同系统版本的适配

在安卓系统版本的升级过程中会伴随着一些接口，以及主题，动画效果的改变，为了适应这些改变
也需要对不同的Android系统版本进行适配,
[点击Android版本](http://developer.android.com/about/dashboards/index.html) 可以看到
Google统计的最新的Android版本情况。
[点击Support Library](http://developer.android.com/tools/support-library/index.html) 可以看到
在每个版本所做的向下兼容包的更新情况。

可以通过minSdkVersion和targetSdkVersion来设定Android app所支持的最低和最高Android版本

也可以通过代码在运行时，根据不同的代码运行不同的逻辑，如下

    private void setUpActionBar() {
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB) {
          ActionBar actionBar = getActionBar();
          actionBar.setDisplayHomeAsUpEnabled(true);
      }
    }

还可以通过相对应主题的设定要使Android app的风格适应于最新版本的Android系统。

    <activity android:theme="@style/xxx">
    <application android:theme="@style/xxx">
