+++
title = "WebView实现Android Hybrid App"
date = "2016-03-16T15:38:50+08:00"
tags = ["Android"]
categories = ["Android"]
menu = ""
banner = "http://7xrnow.com1.z0.glb.clouddn.com/blog_banner_webview.jpg"
+++

WebView+h5+js是实现Adnroid动态化的一种最简单的形式，是通过WebView这个控件来显示html，
再通过跟js的相互调用，从而实现app的动态化。

<!--more-->

## 1. WebView简介

WebView是Android的一个控件，在4.4之前的版本使用的是webkit引擎，在4.4及以后的版本中，
使用的是Chromium引擎。虽然使用的是不同的引擎，但是保持了对外接口的一致性。

## 2. Webview的定制

### 2.1 WebSetting类
WebSettings用来对WebView的配置进行配置和管理，比如是否可以进行文件操作、缓存的设置、
页面是否支持放大和缩小、是否允许使用数据库api、字体及文字编码设置、是否允许js脚本运行、
是否允许图片自动加载、是否允许数据及密码保存等。

WebSetting对象的获取如下

    WebSettings webSettings = webView.getSettings();

获取到WebSetting对象后就可以对WebView进行配置和管理了。比如：

对javascript的支持

    webSettings.setJavaScriptEnabled(true);

### 2.2 WebViewClient类
WebViewClient会在一些影响内容喧嚷的动作发生时被调用，比如表单的错误提交需要重新提交、
页面开始加载及加载完成、资源加载中、接收到http认证需要处理、页面键盘响应、
页面中的url打开处理等。

WebViewClient的设置如下

    webView.setWebViewClient(new WebViewClient());

这个WebViewClient需要自己去重载里面的一些回调函数，比如网页跳转的函数,将其返回值
，设置为false可以控制网页跳转，只发生在本webview内，而不会调用系统的浏览器进行跳转:

    public boolean shouldOverrideUrlLoading(WebView view, String url) {
            return false;
    }

### 2.3 WebChromeClient类
WebChromeClient会在一些影响浏览器ui交互动作发生时被调用，比如WebView关闭和隐藏、
页面加载进展、js确认框和警告框、js加载前、js操作超时、webView获得焦点等

WebChromeClient的设置如下

    webView.setWebChromeClient(new WebChromeClient());

具体的使用方法如同WebViewClient一样，需要自己去重载其中的一些回调函数。

## 3. Android代码与js代码的交互
### 3.1 js调用Android代码

首先设置被js中调用的接口类

    webView.addJavascriptInterface(new JavascriptInterface(), "webfunction");

接口类的实现如下

    class JavascriptInterface {
        @android.webkit.JavascriptInterface
        public void jsUseAndroid(String tip) {
            Toast.makeText(MainActivity.this, "js调用android代码:" + tip, Toast.LENGTH_LONG).show();
        }
    }

在js中调用android代码

     webfunction.jsUseAndroid('I am from js!');

### 3.2 Android调用js代码

相比较为简单，如下

    webView.loadUrl("javascript:usedByAndroid('I am from Android!')");

## 4. 对WebView中的html与js代码进行调试

在Android4.4以后的版本后，即可使用chrome对webview进行调试。如下设置WebView:

    if (Build.VERSION.SDK_INT >=Build.VERSION_CODES.KITKAT) {
        WebView.setWebContentsDebuggingEnabled(true);
    }

在chrome中输入

    chrome://inspect

开启手机的USB debugging模式

运行程序，即可看见相应的运行网站，点击对应inspect，即可开始调试

## 5. WebView的缓存

### 5.1 网页缓存(存储打开过的页面和资源)
 缓存的模式

* LOAD_CACHE_ONLY:  不使用网络，只读取本地缓存数据
* LOAD_DEFAULT:  根据cache-control决定是否从网络上取数据。
* LOAD_CACHE_NORMAL: API level 17中已经废弃, 从API level 11开始作用同LOAD_DEFAULT模式
* LOAD_NO_CACHE: 不使用缓存，只从网络获取数据.
* LOAD_CACHE_ELSE_NETWORK，只要本地有，无论是否过期，或者no-cache，都使用缓存中的数据。

如何设置,建议缓存策略为，判断是否有网络，有的话，使用LOAD_DEFAULT，无网络时，
使用LOAD_CACHE_ELSE_NETWORK。如下：

    //设置缓存模式
    if(Utils.checkNetworkAvailable(this)) {
        webView.getSettings().setCacheMode(WebSettings.LOAD_DEFAULT);
    } else {
        webView.getSettings().setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);
    }

在退出程序前清除缓存

    //清除缓存
    webView.clearCache(true);

### 5.2 H5缓存

#### AppCache缓存

设置缓存路径

    webView.getSettings().setAppCachePath(cacheDirPath);

设置缓存模式，true为打开，false为关闭，默认为false

    webView.getSettings().setAppCacheEnabled(true);

清除缓存，删除设置缓存路径下的文件即可

控制大小

    webView.getSettings().setAppCacheMaxSize(10 * 1024 * 1024);

#### LocalStorage缓存

开启 DOM storage API 功能

    webView.getSettings().setDomStorageEnabled(true);

开启 database storage API 功能

    webView.getSettings().setDatabaseEnabled(true);

## 6. Android WebView 遇到的一些坑

### 生命周期与Android组件不联动

表现为：
退出activity以后webview的声音还在继续响

解决办法：
不在xml文件中定义WebWiew，而是使用动态加载的方式载入WebView。

    webView = new WebView(getApplicationContext());
    llWebview.addView(webView, new ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));

在activity销毁时，手动销毁webview。

    llWebview.removeAllViews();
    webView.destroy();
    webView = null;
    webView.loadUrl(null);
    llWebview = null;

### 给WebView的应用组件一个单独的进程

表现为：
Web的崩溃导致整个应用崩溃，有一些手机再次载入网页出现白屏，无法载入

解决办法：
设置该应用组件为单一的进程

    android:process="com.package.name"

在activity销毁时，销毁这个进程

    System.exit(0);

### 有时需要给WebView添加cookie

表现为:
WebView不像iOS一样同步网络请求的Cookie，需要自行添加Cookie

解决办法:
自行添加Cookie如下:

    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.setAcceptCookie(true);
    cookieManager.removeAllCookie();
    cookieManager.setCookie(url, cookieString);
    CookieSyncManager.getInstance().sync();
    
## 8. Demo地址
https://github.com/lz69/WebViewSummary-Demo
