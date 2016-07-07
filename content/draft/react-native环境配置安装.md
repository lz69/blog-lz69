+++
title = "react-native在ubuntu下环境配置安装"
date = "2016-06-02T15:24:33+08:00"
tags = ["react-native"]
categories = ["react-native"]
menu = ""
+++

学习react-native第一步，就是安装react-native的环境。
<!--more-->

## Node.js的安装
Node.js是一个基于Chrome JavaScript运行时建立的一个平台。
运行命令

    sudo apt-get install nodejs

nodejs安装后的命令为nodejs，需要重nodejs程序建立一个链接为node才能让react-native运行正常

    ln -s nodejs node in /usr/bin

## watchman的安装
Watchman 是 facebook 的一个开源项目，它开源用来监视文件并且记录文件的改动情况，当文件变更它可以触发一些操作,例如执行一些命令等等

从源码安装

安装相关依赖

    sudo apt-get install autoconf  automake python-dev

clone github上watchman的源码

    git clone https://github.com/facebook/watchman.git

编译watchman

    cd watchman
    ./autogen.sh
    ./configure
    make

安装watchman

    sudo make install

## npm的安装
npm是node.js的包管理工具

运行命令

    sudo apt-get install npm

## 利用npm安装react-native
运行命令

    npm install -g react-native-cli
