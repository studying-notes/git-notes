---
date: 2020-10-11T21:00:35+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "解决 Git HEAD 游离状态"  # 文章标题
# description: "HEAD 游离状态"
url:  "posts/git/abc/head"  # 设置网页永久链接
tags: [ "git", "head"]  # 标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: true  # 草稿
---

## 什么是 HEAD

Git 中的 HEAD 可以理解为一个指针，我们可以在命令行中输入 `cat .git/HEAD` 查看当前 HEAD 指向哪儿，一般它指向当前工作目录所在分支的最新提交。

当使用 `git checkout <branch>` 切换分支时，HEAD 会移动到指定分支。

但是如果使用的是 `git checkout <commit id>`，即切换到指定的某一次提交，HEAD 就会处于 `detached` 状态（游离状态）。

## 游离状态的利与弊

HEAD 处于游离状态时，我们可以很方便地在历史版本之间互相切换，比如需要回到某次提交，直接 `checkout` 对应的 `commit id` 或者 `tag` 名即可。

它的弊端就是：在这个基础上的提交会新开一个匿名分支。也就是说我们的提交是无法可见保存的，一旦切到别的分支，游离状态以后的提交就不可追溯了。

## 解决方法

暂未解决

```shell

```

```shell

```

```shell

```

```shell

```

```shell

```

```shell

```

