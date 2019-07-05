---
title: Git小白指令
date: 2019-07-05 02:08:43
tags:
    -Git笔记
---
&nbsp;&nbsp;&nbsp;&nbsp;因为最近写博客，需要上传GitHub,所以一直在花时间去学习，现在已经凌晨两点了，之所以还在坚持写，不为别的，只为弥补第一篇心得里面吹下的牛皮。
&nbsp;&nbsp;&nbsp;&nbsp;关于Git的指令，参照廖雪峰老师的教程来的，然后下面记录一下

* git add ./xxx.txt  这个表示将写好的代码添加到本地的仓库 ，add . 表示直接添加目录下所有文件
* git commit -m "提交日志"  这个命令表示将添加到本地仓库的代码提交 ，
* git push -u origin master 表示将本地仓库的代码提交到github远程仓库，
* git pull origin master 表示将远程仓库的代码拉取与本地代码进行合并，
* git status  这个命令可以让我们了解当前仓库的状态，哪些文件已经修改但是还没有提交，
* git log 表示查看提交到git仓库的所有版本，
* git branch dev(分之的名称) 创建一个新的分支
* git checkout dev 选中新创建的分之进行操作
* git merge dev 在切换到master分支上 进行将dev分支的操作合并到master分支上
* git branch -d dev 将刚才已经操作过的分支删除
* git branch 查看当前所有分支


<center>未完待续.....</center>
