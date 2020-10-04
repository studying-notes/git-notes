---
date: 2020-09-19T21:32:00+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 撤销操作"  # 文章标题
description: "Git 撤销上一步提交操作，撤销暂存"
url:  "posts/2020/09/19/gitreset"  # 设置网页链接，默认使用文件名
tags: [ "git", "command"] # 自定义标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---

## 撤销提交

撤销上一步提交操作：

```shell
git reset [flag] HEAD^
```

`HEAD^` 表示上一次 `commit` 操作，如果想撤销两次 `commit` 操作，可以改为 `HEAD~2`。

- `--mixed` - 不删除工作空间改动代码，撤销 `commit`，并且撤销 `git add .` 操作，默认参数
- `--soft  ` - 不删除工作空间改动代码，撤销 `commit`，不撤销 `git add .`
- `--hard` - 删除工作空间改动代码，撤销 `commit`，撤销 `git add .`


```shell
git reset --soft HEAD^
```

```shell
git reset HEAD^
```

```shell
git reset --hard HEAD^
```

## 撤销暂存

以下命令可以撤销暂存的更改，就是已经 `git add <file>` 但是还未 `git commit -m ""` 的情形：

```shell
git restore --staged <file>
```
