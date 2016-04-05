+++
title = "Service的自启动"
date = "2016-04-01T13:54:48+08:00"
tags = ["Android"]
categories = ["技术相关"]
menu = ""
+++

我们在使用Android应用的时候，会发现有一些相应的Service也会随之启动，有些应用会随着
开机自启动一些服务，有些应用的服务被关闭以后，过一段时间又会自行启动，甚至还存在一些
应用之间的相互唤醒。我觉得作为一个开发者有必要去了解这些功能是如何实现的。

<!--more-->

## 开机自启

这个比较简单，大概思路是实现一个BroadcastReceiver，监听手机完成开机的事件ACTION_BOOT_COMPLETED
后，启动一个Service即可。

第一步：实现一个BroadcastReceiver，并且在其中加入启动Service相应的逻辑。

    @Override
    public void onReceive(Context context, Intent intent) {
      Intent intentService = new Intent(context, SelfStartingService.class);
      context.startService(intentService);
    }

第二步：注册BroadcastReceiver，并且在加入相关的intent-filter配置

第三步：注册权限
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
