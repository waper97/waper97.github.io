---
title: git常见问题
date: 2021-12-08 14:52:12
tags: git常用命令
categories: git
comments: true

---

## git常见问题

<!--more-->

## 1.恢复数据相关

#### 1.1git恢复未提交的误删数据

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





## 2.撤销相关

#### 2.1 git撤销操作

```
git commit -amend
```

amend v. 修改、修正

#### 2.2取消已经暂存的文件

```shell
git reset HEAD <fileName>
```

或者

```shell
git restore --staged <file>
```

![image-20211217100629615](https://raw.githubusercontent.com/waper97/Pic-Go/main/img/202112201032386.png)	

### 取消对问文件的修改

**注意：** 恢复文件的所有修改，请确保这个要恢复的文件真的不需要再保留，否则会丢失你修改的内容

```shell
git checkout -- benchmarks.rb
```





## 3.合并相关

#### 3.1.项目分叉历史:

`git log` 查看日志

`git log --oneline --decorate --graph --all`   它会输出你的提交历史、各个分支的指向以及项目的分支分叉情况。

```shell
$ git log --oneline --decorate --graph --all
* 88d25ec (HEAD -> main) made other changes
| * 04ccf5c (testing) made a change
|/
* db17c65 (tag: v1.1, tag: v1.0, origin/main, origin/HEAD) add dogs.gif
* 03ff68b add jrebel piture
* ab06611 添加动漫妹子图片一张
```

==**Note:**==

创建新分支的同时切换过去

通常我们会在**创建一个新分支后立即切换过去**，这可以用 `git checkout -b <newbranchname>` 一条命令搞定。





#### 3.2 **删除分支** -d 选项

```
$ git branch -d hotfix
Deleted branch hotfix (was 4205df4).
```

#### 3.3 合并分支冲突问题

`git merge branch_name`

```bash
$ git merge iss53
CONFLICT (add/add): Merge conflict in index.html
Auto-merging index.html
Automatic merge failed; fix conflicts and then commit the result.
```

先查看一下状态 `git status`

```bash
$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      index.html
```

> 任何因包含合并冲突而有待解决的文件，都会以未合并状态标识出来。 Git 会在有冲突的文件中加入标准的冲突解决标记，这样你可以打开这些包含冲突的文件然后手动解决冲突。 出现冲突的文件会包含一些特殊区段，看起来像下面这个样子：

```bash
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

这表示 `HEAD` 所指示的版本（也就是你的 `master` 分支所在的位置，因为你在运行 merge 命令的时候已经检出到了这个分支）在这个区段的上半部分（`=======` 的上半部分），而 `iss53` 分支所指示的版本在 `=======` 的下半部分。 为了解决冲突，你必须选择使用由 `=======` 分割的两部分中的一个，或者你也可以自行合并这些内容。 例如，你可以通过把这段内容换成下面的样子来解决冲突：

```tex
<div id="footer">
please contact us at email.support@github.com
</div>
```

上述的冲突解决方案仅保留了其中一个分支的修改，并且 `<<<<<<<` , `=======` , 和 `>>>>>>>` 这些行被完全删除了。 在你解决了所有文件里的冲突之后，对每个文件使用 `git add` 命令来将其标记为冲突已解决。 一旦暂存这些原本有冲突的文件，Git 就会将它们标记为冲突已解决。

如果你想使用图形化工具来解决冲突，你可以运行 `git mergetool`，该命令会为你启动一个合适的可视化合并工具，并带领你一步一步解决这些冲突：

```
Administrator@BF-202102221111 MINGW64 /d/SOFT/picture (main|MERGING)
$ git mergetool


This message is displayed because 'merge.tool' is not configured.
See 'git mergetool --tool-help' or 'git help config' for more details.
'git mergetool' will now attempt to use one of the following tools:
opendiff kdiff3 tkdiff xxdiff meld tortoisemerge gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare smerge emerge vimdiff nvimdiff
Merging:
index2.html

Normal merge conflict for 'index2.html':
  {local}: modified file
  {remote}: modified file
Hit return to start merge resolution tool (tortoisemerge):

```



#### 3.2 git 本地分支和远程分支如何关联

```
git branch origin 分支名称
```







## 4.推送相关

#### 4.1推送代码到远程

```shell
git push orgin 分支名
```

#### 4.2





## 5.克隆相关

#### 5.1git 克隆分支代码

```shell
git clone -b 分支名 http://(git@github.comXXXX.git)
```



### 6.远程仓库的使用

#### 6.1 查看当前远程仓库

​	**git remote -v**

 ```
 $ git remote -v
 origin  git@github.com:waper97/waper97.github.io.git (fetch)
 origin  git@github.com:waper97/waper97.github.io.git (push)
 ```

#### 6.2 添加远程仓库

**git remote add [shortname] [url]**



#### 6.3 从远程仓库抓取数据

```shell
git fetch [remote-name]
```

#### 6.4 查看远程仓库信息

```shell
git remote show [remote_name]
```

