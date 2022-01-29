---
date: 2022-01-29T09:37:54+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 更改提交操作"  # 文章标题
# description: "文章描述"
url:  "posts/git/quickstart/modify"  # 设置网页永久链接
tags: [ "git", "github", "gitlab", "quickstart"] # 自定义标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

## git reset

回溯历史版本。

Git 的另一特征便是可以灵活操作历史版本。借助分散仓库的优势，可以在不影响其他仓库的前提下对历史版本进行操作。

在这里，为了让各位熟悉对历史版本的操作，我们先回溯历史版本，创建一个名为 fix-B 的特性分支（图 4.4）。

1. 回溯到创建 feature-A 分支前

要让仓库的 HEAD、暂存区、当前工作树回溯到指定状态，需要用到 git reset --hard 命令。只要提供目标时间点的哈希值 ，就可以完全恢复至该时间点的状态。

```shell
git reset --hard fd0cbf0
```

2. 创建 fix-B 分支

```shell
git checkout -b fix-B
```

现在的状态如图 4.5 所示。接下来我们的目标是图 4.6 中所示的状态，即主干分支合并 feature-A 分支的修改后，又合并了 fix-B 的修改。

![](../assests/images/图%204.5_当前fix-B分支的状态.png)

![](../assests/images/图%204.6_fix-B分支的下一步目标.png)

3. 推进至 feature-A 分支合并后的状态

首先恢复到 feature-A 分支合并后的状态。不妨称这一操作为“推进历史”。

git log 命令只能查看以当前状态为终点的历史日志。所以这里要使用 git reflog 命令，查看当前仓库的操作日志。在日志中找出回溯历史之前的哈希值，通过 git reset -- hard 命令恢复到回溯历史前的状态。

```shell
git reflog
```

查看当前仓库执行过的操作的日志。

在日志中，我们可以看到 commit、checkout、reset、merge 等 Git 命令的执行记录。只要不进行 Git 的 GC（Garbage Collection，垃圾回收），就可以通过日志随意调取近期的历史状态，就像给时间机器指定一个时间点，在过去未来中自由穿梭一般。即便开发者错误执行了 Git 操作，基本也都可以利用 git reflog 命令恢复到原先的状态。

feature-A 特性分支合并后的状态对应哈希值为 83b0b94。我们将 HEAD、暂存区、工作树恢复到这个时间点的状态。

```shell
git reset --hard 83b0b94
```

之前我们使用 git reset -- hard 命令回溯了历史，这里又再次通过它恢复到了回溯前的历史状态。

![](../assests/images/图%204.7_恢复历史后的状态.png)

## 消除冲突

现在只要合并 fix-B 分支，就可以得到我们想要的状态。

```shell
git merge ——no-ff fix-B
```

这时，系统告诉我们 README.md 文件发生了冲突（Conflict）。系统在合并 README.md 文件时，feature-A 分支更改的部分与本次想要合并的 fix-B 分支更改的部分发生了冲突。

不解决冲突就无法完成合并，所以我们打开 README.md 文件，解决这个冲突。

冲突解决后，执行 git add 命令与 git commit 命令。

由于本次更改解决了冲突，所以提交信息记为 "Fix conflict"。

## git commit --amend

要修改上一条提交信息，可以使用 git commit --amend 命令。

我们将上一条提交信息记为了 "Fix conflict"，但它其实是 fix-B 分支的合并，解决合并时发生的冲突只是过程之一，这样标记实在不妥。于是，我们要修改这条提交信息。

```shell
git commit --amend
```

```shell
git config --global core.editor 'vim'
```

执行上面的命令后，编辑器就会启动。将提交信息的部分修改为 Merge branch 'fix-B'，然后保存文件，关闭编辑器。

## git rebase -i

压缩历史。

在合并特性分支之前，如果发现已提交的内容中有些许拼写错误等，不妨提交一个修改，然后将这个修改包含到前一个提交之中，压缩成一个历史记录。

1. 创建 feature-C 分支

```shell
git checkout -b feature-C
```

作为 feature-C 的功能实现，我们在 README.md 文件中添加一行文字，并且故意留下拼写错误，以便之后修正。

提交这部分内容。这个小小的变更就没必要先执行 git add 命令再执行 git commit 命令了，我们用 git commit -am 命令来一次完成这两步操作。

```shell
git commit -am "Add feature-C"
```

2. 修正拼写错误

```shell
git commit -am "Fix typo"
```

错字漏字等失误称作 typo，所以我们将提交信息记为 "Fix typo"。

实际上，我们不希望在历史记录中看到这类提交，因为健全的历史记录并不需要它们。如果能在最初提交之前就发现并修正这些错误，也就不会出现这类提交了。

3. 更改历史

因此，我们来更改历史。将 "Fix typo" 修正的内容与之前一次的提交合并，在历史记录中合并为一次完美的提交。为此，我们要用到 git rebase 命令。

```shell
git rebase -i HEAD～2
```

用上述方式执行 git rebase 命令，可以选定当前分支中包含 HEAD（最新提交）在内的两个最新历史记录为对象，并在编辑器中打开。

```shell
pick 7a34294 Add feature-C
pick 6fba227 Fix typo
```

我们将 6fba227 的 Fix typo 的历史记录压缩到 7a34294 的 Add feature-C 里。按照下图所示，将 6fba227 左侧的 pick 部分删除，改写为 fixup。

```shell
pick 7a34294 Add feature-C
fixup 6fba227 Fix typo
```

保存编辑器里的内容，关闭编辑器。

系统显示 rebase 成功。也就是以下面这两个提交作为对象，将 "Fix typo" 的内容合并到了上一个提交 "Add feature-C" 中，改写成了一个新的提交。

现在再查看提交日志时会发现 Add feature-C 的哈希值已经不是 7a34294 了，这证明提交已经被更改。

这样一来，Fix typo 就从历史中被抹去，也就相当于 Add feature-C 中从来没有出现过拼写错误。这算是一种良性的历史改写。
