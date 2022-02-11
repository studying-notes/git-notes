---
date: 2022-01-29T09:01:43+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 基本操作"  # 文章标题
# description: "文章描述"
url:  "posts/git/quickstart/operation"  # 设置网页永久链接
tags: [ "git", "github", "gitlab", "quickstart" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

## git init

初始化仓库，如果初始化成功，执行了 git init 命令的目录下就会生成 .git 目录。这个 .git 目录里存储着管理当前目录内容所需的仓库数据。

在 Git 中，我们将这个目录的内容称为“附属于该仓库的工作树”。文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。如果想将文件恢复到原先的状态，可以从仓库中调取之前的快照，在工作树中打开。开发者可以通过这种方式获取以往的文件。

## git status

显示 Git 仓库的状态。工作树和仓库在被操作的过程中，状态会不断发生变化。

## git add

向暂存区中添加文件。

如果只是用 Git 仓库的工作树创建了文件，那么该文件并不会被记入 Git 仓库的版本管理对象当中。因此我们用 git status 命令查看 README.md 文件时，它会显示在 Untracked files 里。

要想让文件成为 Git 仓库的管理对象，就需要用 git add 命令将其加入暂存区（Stage 或者 Index）中。暂存区是提交之前的一个临时区域。

将 README.md 文件加入暂存区后，git status 命令的显示结果发生了变化。可以看到，README.md 文件显示在 Changes to be committed 中了。

## git commit

保存仓库的历史记录。

git commit 命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。

## git log

git log 命令可以查看以往仓库中提交的日志。包括可以查看什么人在什么时候进行了提交或合并，以及操作前后有怎样的差别。

## git diff

git diff 命令可以查看工作树、暂存区、最新提交之间的差别。

“+”号标出的是新添加的行，被删除的行则用“-”号标出。

如果执行 git diff 命令时，由于工作树和暂存区的状态并无差别，结果什么都不会显示。

要查看与最新提交的差别，请执行以下命令。

```shell
git diff HEAD
```
