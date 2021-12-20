---
title: git常见问题
date: 2021-12-08 14:52:12
tags: git常用命令
categories: git
comments: true

---

## git常用命令
<!--more-->

| 命令 | 含义 |
| :--: | :--: |
|      |      |
|      |      |





# git常见问题

### **git恢复未提交的误删数据**

```shell
$ git reflog
```

```shell
$ git reflog
be2f967 (HEAD -> hexo, origin/hexo) HEAD@{0}: reset: moving to be2f9672e7c0ee9cd8f67216fcb16eeeb149db6e
be2f967 (HEAD -> hexo, origin/hexo) HEAD@{1}: checkout: moving from master to hexo
bb16153 (origin/master, origin/HEAD, master) HEAD@{2}: checkout: moving from hexo to master
bb16153 (origin/master, origin/HEAD, master) HEAD@{3}: checkout: moving from master to hexo
bb16153 (origin/master, origin/HEAD, master) HEAD@{4}: clone: from github.com:waper97/waper97.github.io.git

```

**git reflog`/`git log -g**可以查看所有历史操作记录

可以通过 **git reset** 命令恢复

```shell
$ git reset --hard be2f967
HEAD is now at be2f967 添加hexo源文件

Administrator@BF-202102221111 MINGW64 /d/SOFT/hexo/waper97.github.io (hexo)
$ git status
On branch hexo
Your branch is up to date with 'origin/hexo'.

nothing to commit, working tree clean
```

然后就大功告成啦！



git 本地分支和远程分支如何关联

```
git branch origin 分支名称
```

`git push 分支`到远程 

```shell
git push orgin 分支名
```



git 克隆分支代码

```
git clone -b 分支名 http://(git@github.comXXXX.git)
```







### git撤销操作

```shell
git commit -amend
```

amend v. 修改、修正



### 取消已经暂存的文件

```shell
git reset HEAD <fileName>
```

或者

```shell
git restore --staged <file>
```

![image-20211217100629615](D:\SOFT\waper97.github.io\source\_posts\git常用命令\image-20211217100629615.png)	

### 取消对问文件的修改

**注意：** 恢复文件的所有修改，请确保这个要恢复的文件真的不需要再保留，否则会丢失你修改的内容

```shell
git checkout -- benchmarks.rb
```

