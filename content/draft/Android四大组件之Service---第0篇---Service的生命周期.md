+++
title = "Android四大组件之Service---第0篇---Service的生命周期"
date = "2016-03-09T17:35:33+08:00"
tags = ["Android"]
categories = ["技术相关"]
menu = ""
+++

Service是Android的四大组件之一，它长期运行在系统的后台，而不与用户产生交互。

<!--more-->

## 1.Serive的生命周期
### 1.1 startService()
通过startService()运行Service时，应用的组件跟该Service不能产生互动。通常用这样的
Service来下载或者上传文件，当任务完成时，应该stopService()。

当第一次调用startService()时，首先会调用Service的构造函数创建一个Service
的实例，接着调用onCreate()函数，最后通过onStartCommand()函数启动Service。

    StartToService() ->  onCreate() -> onStartCommand()

之后在没有stopService的情况下，继续startService(),Service只会回调
onStartCommand()。

    onStartCommand()

当调用stopService()时,Service会直接回调onDestory()方法销毁Service。

    onDestory()

### 1.2 bindService()
只有已经被startService()的Service，才能通过bindService()绑定Service时，应用的
组件是可以跟Serice产生互动的。应用组件相当于是client，被绑定的Service相当于是
Service，他们之间是一种c-s结构。一个Service可以同时被多个应用组件绑定，在销毁
前(stopService()),它会解除和所有的应用组件的绑定。

在已经运行的Serivce，绑定应用组件，会先回调该Service的onBind()方法，然后会回调
应用组件中的ServiceConnection实例的onServiceConnected()方法。

    onBind() -> onServiceConnected()

直接调用stopService()销毁Service,它会解除所有的绑定后，再进行销毁。先回调应用组件
中的ServiceConnection实例的onSeviceDisconnected()方法，再回调Service的
onUnBind()方法，最后回调onDestory()方法销毁自身。

    onSeviceDisconnected() -> onUnBind() -> onDestory()

在已经bindService()的情况下，调用unBindService()方法对Service进行接触绑定。只会
调用onUnBind()方法。

    onUnBind()

//有疑问
在之前已经绑定过该Service，但后来unBindService()的情况下进行bindService()。只会
回调应用组件中的ServiceConnection实例的onServiceConnected()方法。

    onServiceConnected()
