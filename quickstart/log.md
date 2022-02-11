---
date: 2020-09-19T21:32:00+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 显示提交历史"  # 文章标题
description: "Git 显示提交历史，自定义输出格式"
url:  "posts/git/quickstart/log"  # 设置网页链接，默认使用文件名
tags: [ "git", "command" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---

## 显示提交历史

```shell
# 单行显示
git log --pretty=oneline
```

```shell
# 最大数量
git log --pretty=oneline --max-count=2
```

```shell
# 从几分钟前开始
git log --pretty=oneline --since='5 minutes ago'
```

```shell
# 到几分钟前结束
git log --pretty=oneline --until='5 minutes ago'
```

```shell
# 指定某人的提交记录
git log --pretty=oneline --author=<your name>
```

```shell
# 全部显示
git log --pretty=oneline --all
```

## 显示全部提交历史

有时候进行了误操作，撤销了某次提交，这时候 git log 是不显示这个操作的。

```shell
git relog
```

## 自定义输出格式

- `--pretty="..."` 定义输出的格式
- `%h` 提交 HASH 的前几位
- `%d` 提交的分支头或标签
- `%ad` 创作日期
- `%s` 注释
- `%an` 作者姓名
- `--graph` 使用 ASCII 图形布局显示提交树
- `--date=short` 更短的日期形式

输出七天之内提交的更改：

```shell
git log --all --pretty=format:'%h %cd %s (%an)' --since='7 days ago'
```

一个不错的全部提交历史显示格式：

```shell
git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```
