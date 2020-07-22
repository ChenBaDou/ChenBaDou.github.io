---
layout: post
title: "前端小Tip之移除SourceTree无用的远程分支"
date: 2020-07-14 21:00:08 +0800
description: 前端小Tip之移除SourceTree无用的远程分支
tags: [前端,小Tip]
img: import/SourceTree.jpg
---

### 移除 SourceTree 无用的远程分支

在开发过程中我们很多时候都需要将当前分支推送到远程仓库，该分支完成其使命之后再将其删除。
使用 SourceTree 的同学可能会发现 SourceTree 追踪的远端分支越来越多，许多已经删除的分支也还在，即使从 origin 重新拉取也不行。
虽然这些不影响正常的使用，但想快速的找到一个分支还是有点麻烦的，于是我们决定清除它们。

### 解决方法
1、进入对应目录下，使用  `git remote show origin`  命令查看本地仓库追踪远程仓库的状态
2、使用  `git remote prune origin`  清除所有失效的远程分支或根据提示删除特定失效分支
3、重启 SourceTree 即可。
