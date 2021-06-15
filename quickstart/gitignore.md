---
date: 2021-03-11T08:43:49+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: ".gitignore 忽略文件"  # 文章标题
description: "Git 忽略文件"
url:  "posts/git/quickstart/gitignore"  # 设置网页链接，默认使用文件名
tags: [ "git", "command"] # 自定义标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

```ini
# you can skip this first one if it is not already excluded by prior patterns
!application/

application/*
!application/language/

application/language/*
!application/language/gr/
```

尾随 `/*` 很重要：

- 模式 `dir/` 排除名为 `dir` 和其下的所有内容。
使用 `dir/`，Git 永远不会在 `dir` 下查看任何内容，因此永远不会将任何 “un-exclude” 模式应用于 `dir` 下的任何内容。
- `dir/*` 模式没有说明 `dir` 本身; 它只是排除了 `dir` 下的所有内容。使用 `dir/*`，Git 将处理 `dir` 的直接内容，使其他模式有机会 “取消排除” 某些内容（ `!dir/sub/` ）。

