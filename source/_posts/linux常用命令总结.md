---
title: linux常用命令总结
date: 2021-12-03 09:59:54
tags: linux常用命令
categories: linux常用命令
comments: true
---

#### linux各目录含义

![image-20211223144545818](https://raw.githubusercontent.com/waper97/Pic-Go/main/img/202112231445038.png)

```  java
boot: 内核  引导加载程序文件
home: 用户home路径 用户主目录
tmp:  临时文件
var ：日志文件 变量文件
usr :应用程序目录 用户程序
opt: 可选的附加应用程序
swap : 交换分区	
media : 媒体。(用于挂载可移动设备的临时目录。)
etc ： 配置文件 存放程序所需要的所有配置文件
proc ：进程信息	
dev ： 设备文件
bin : 用户二进制文件
sbin: 系统二进制文件
```

#### linux常用命令总结

<!--more-->

{% codeblock %}

Ctrl+a 移动到当前行的开头

Ctrl+e 移动到当前行的结尾


Ctrl+l 清屏

Ctrl+u 剪切命令行中光标所在处之前的所有字符（不包括自身）

Ctrl+k 剪切命令行中光标所在处之后的所有字符（包括自身）

Ctrl+d 删除光标所在处字符

Ctrl+(x u) 按住Ctrl的同时再先后按x和u，撤销刚才的操作

Ctrl+s 挂起当前shell

Ctrl+q 退出挂起shell

Ctrl + u  删除光标之前到行首的字符
Ctrl + k  删除光标之前到行尾的字符
{% endcodeblock %}

###  查看当前内存使用情况

``` shell
free -m
```

###  top命令

```
shift+m 显示占用内存百分比
```



