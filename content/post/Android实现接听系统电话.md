+++
title = "Android实现接听系统电话的研究"
date = "2016-03-17T15:16:50+08:00"
tags = ["Android"]
categories = ["Android"]
menu = ""
+++

Android实现系统电话接听有两种思路，第一种思路是使用ITelephony中的answerRingingCall()方法，
第二中思路是模拟耳机接听电话的事件，这里又分两种方式实现模拟这个时间，第一种为发送该事件的广播，
第二种是直接运行脚本命令实现这个事件的模拟。

<!--more-->

## 1. ITelephony的answerRingingCall()方法实现

调用此方法需要android.permission.MODIFY_PHONE_STATE权限，但是在Android2.3及以上版本，这个
权限为系统应用权限，普通应用无法进行调用。所以这种方式是行不通的。

## 2. 模拟耳机接听电话事件

### 2.1 发送模拟耳机接听电话事件系统广播

实现代码:

    Intent intent = new Intent("android.intent.action.MEDIA_BUTTON");
    KeyEvent keyEvent = new KeyEvent(KeyEvent.ACTION_UP, KeyEvent.KEYCODE_HEADSETHOOK);
    intent.putExtra("android.intent.extra.KEY_EVENT", keyEvent);
    sendOrderedBroadcast(intent, "android.permission.CALL_PRIVILEGED");

注意在这种方式下发送这个广播需要android.permission.CALL_PRIVILEGED权限，但这这个权限在Android4.1
以上(经测试，5.0及以上系统这种方法基本行不通，4.1-5.0之间有部分手机可行)，也需要系统应用才能够得到，
所以这也不是一个普遍适用的方法。

### 2.2 直接运行脚本命令模拟事件

实现代码:

    try {
        Runtime.getRuntime().exec("input keyevent " + Integer.toString(KeyEvent.KEYCODE_HEADSETHOOK));
    } catch (Exception e) {
        Toast.makeText(this, "接听失败", Toast.LENGTH_LONG).show();
    }

亲测在cm的Android6.0下可行。
