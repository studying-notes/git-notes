---
date: 2020-09-19T21:32:00+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 变基与合并"  # 文章标题
url:  "posts/2020/09/19/gitrebase"  # 设置网页链接，默认使用文件名
tags: [ "git", "command"] # 自定义标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---

变基的最终结果与合并很相似。然而，提交树却十分不同。dev 分支的提交树已被重写，以致 master 分支成为了其提交历史的一部分。这使提交链更加线性，且更易阅读。

公开且与其他人共享的分支，重写公开的共享分支将会搞砸团队中的其他成员。因此针对短期生命的本地分支使用变基，而对公开仓库的分支使用合并。

## 合并

`git merge dev`

```shell
git hist
```

```
* f9b8c57 2020-07-26 | done (HEAD -> master) [Rustle Karl]
*   4717168 2020-07-26 | 冲突 [Rustle Karl]
|\
| * b89ee5b 2020-07-26 | m (dev) [Rustle Karl]
| * 0eecbca 2020-07-26 | ok [Rustle Karl]
* | 6cae58f 2020-07-26 | ok [Rustle Karl]
* | 1d547ea 2020-07-26 | ok [Rustle Karl]
|/
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]
```

## 变基

将 master 中的更改集成到 dev 分支，用 rebase 命令代替 merge 命令来从 master 分支中引入更改。

`git rebase master`

```shell
git checkout dev
```

```shell
git hist
```

```
* b89ee5b 2020-07-26 | m (HEAD -> dev) [Rustle Karl]
* 0eecbca 2020-07-26 | ok [Rustle Karl]
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]
```

```shell
git rebase master
```

```
Successfully rebased and updated refs/heads/dev.
```

```shell
git hist
```

```
* 4a7b43a 2020-07-26 | done (HEAD -> dev, master) [Rustle Karl]
* f9b8c57 2020-07-26 | done [Rustle Karl]
*   4717168 2020-07-26 | 冲突 [Rustle Karl]
|\
| * b89ee5b 2020-07-26 | m [Rustle Karl]
| * 0eecbca 2020-07-26 | ok [Rustle Karl]
* | 6cae58f 2020-07-26 | ok [Rustle Karl]
* | 1d547ea 2020-07-26 | ok [Rustle Karl]
|/
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]
```
