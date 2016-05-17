+++
title = "Linux相关总结---第0篇---shell基础语法"
date = "2016-03-07T17:35:33+08:00"
tags = ["linux"]
categories = ["Linux"]
menu = ""
banner = "http://7xrnow.com1.z0.glb.clouddn.com/blog_shell.png"
+++

shell script是利用shell的功能所写的一个程序，这个程>序是使用纯文本文件，将一些shell的语法与指令写在里面，然后用正规表示法，管道命令以及数据流重导向等功能，以达到我们所想要的处理目的。更明白地来说，shell script就像早期dos年代的.bat，最简单的功能就是将许多指令汇整写一起，让使用者很容易地就能够一个操作执行多个命令，而shell script更是提供了数组，循环，条件以及逻辑判断等重要功能，让使用者可以直接以shell来写程序，而不必使用类似C程序语言等传统程序编写的语法。
<!--more-->
## 1.执行Shell命令
    1. ./*.sh
    2. sh *.sh
    3. chmod u+x *.sh

## 2.shell脚本的注释已#开头
    #我是注释

## 3.变量（定义变量时等号不要有空格）
### 字符串变量
    str="string"
### 数字变量
    num=666
### 获取变量
    echo "number = $num", "str = $str."
### 删除变量
    variable_name="www.leonzou.com"
    unset variable_name
    echo ${variable_name}
### 系统变量
    $0 这个程序的执行名字
    $n 这个程序的第n个参数值，n=1...9
    $* 这个程序的所有参数
    $# 这个程序的参数个数
    $$ 这个程序的PID
    $! 执行上一个背景指令的PID
    $? 上一个指令的返回值

## 4.双引号及单引号
### 显示变量值
    $echo "$PATH"
### 显示单引号里的内容
    $echo '$PATH'

## 5.运算
### 数字运算
    expr ${num} + 1
    expr ${num} - 1
    expr ${num} \* 1
    expr ${num} / 1
    expr1 % expr2
### 逻辑运算（成立则传回1，不成立传回0）
    int1 -eq int2 相等? expr1 = expr2
    int1 -ne int2 不等? expr1 != expr2
    int1 -gt int2 int1 \> int2 ?
    int1 -ge int2 int1 \>= int2 ?
    int1 -lt int2 int1 \< int2 ?
    int1 -le int2 int1 \<= int2 ?

## 6.分支结构
### if分支
    if [[ true ]]; then
      echo "helloworld"
    elif [[ false ]]; then
      echo "elif"
    else
      echo "else"
    fi
### case分支
    case "w" in
    "w" )
      echo "w"
    ;;
    "o" )
      echo "o"
    ;;
    esac

## 7.循环结构
### for循环
    for (( i = 0; i < 10; i++ )); do
      echo $i
    done

## 8.函数
    setup ()
    { echo setup; }
    do_data ()
    { echo data; }
    setup
    do_data

## 9.从命令行等待输入值
### 普通变量
    read str1 str2 ...
### 只读变量，变量的值不能被改变
    readonly str2
