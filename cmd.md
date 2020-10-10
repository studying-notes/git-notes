---
date: 2020-09-19T21:32:00+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 常用命令列表"  # 文章标题
description: "Git 常用命令列表"
url:  "posts/git/cmd"  # 设置网页链接，默认使用文件名
tags: [ "git", "command"] # 自定义标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---

| 命令 | 作用 |
| ---- | ---- |
| git status | 当前仓库的状态 |
| git add<file> | 暂存更改 |
| git reset HEAD<file> | 取消文件暂存更改 |
| git checkout <file> | 放弃文件更改 |
| git restore --stage<file> | 放弃文件暂存更改 |
| git commit -m | 提交更改 |
| git commit --amend -m | 修正先前的提交 |
| git checkout <hash> | 切换旧版本、切换分支 |
| git tag <tag> | 打标签 |
| git tag -d<tag> | 移除标签 |
| git revert HEAD --no-edit | 撤销最后提交 |
| git reset --hard v1 | 从分支移除提交 |
| git mv <src> <dst> | 移动文件 |
| git mv <old> <new> | 重命名文件/文件夹 |
| git checkout -b <branch> | 创建分支 |
| git branch -d <branch> | 删除分支 |
| git branch -D <branch> | 强制删除分支 |
| git branch -a | 列出全部分支 |
| git branch -m <old> <new> | 重命名分支 |
| git checkout -b <branch> <origin/branch> | 克隆远程分支 |
| git merge <branch> | 合并 |
| git rebase <branch> | 变基 |
| git mv -f oldfolder newfolder | 重命名文件夹 |
