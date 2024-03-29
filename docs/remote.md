---
date: 2022-01-29T10:12:06+08:00  # 创建日期
author: "Rustle Karl"  # 作者

title: "Git 操作远程仓库"  # 文章标题
url:  "posts/git/docs/remote"
tags: [ "Git" ]
categories: [ "Git 学习笔记" ]

toc: true  # 目录
draft: false  # 草稿
---

- [初始化仓库](#初始化仓库)
- [添加远程仓库](#添加远程仓库)
- [推送至远程仓库](#推送至远程仓库)
  - [推送至指定分支](#推送至指定分支)
- [获取远程仓库](#获取远程仓库)
  - [获取远程指定分支](#获取远程指定分支)
- [获取最新的远程仓库分支](#获取最新的远程仓库分支)
- [显示仓库远程地址](#显示仓库远程地址)

## 初始化仓库

```shell
echo "# git-tutorial" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
```

## 添加远程仓库

```shell
git remote add origin git@github.com:studying-notes/git-tutorial.git
```

## 推送至远程仓库

```shell
git push -u origin main
```

-u 参数可以在推送的同时，将 origin 仓库的 master 分支设置为本地仓库当前分支的 upstream（上游）。添加了这个参数，将来运行 git pull 命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从 origin 的 master 分支获取内容，省去了另外添加参数的麻烦。

执行该操作后，当前本地仓库 master 分支的内容将会被推送到 GitHub 的远程仓库中。在 GitHub 上也可以确认远程 master 分支的内容和本地 master 分支相同。

### 推送至指定分支

除了 master 分支之外，远程仓库也可以创建其他分支。举个例子，我们在本地仓库中创建 feature-D 分支，并将它以同名形式 push 至远程仓库。

```shell
git checkout -b feature-D
```

我们在本地仓库中创建了 feature-D 分支，现在将它 push 给远程仓库并保持分支名称不变。

```shell
git push -u origin feature-D
```

现在，在远程仓库的 GitHub 页面就可以查看到 feature-D 分支了。

## 获取远程仓库

执行 git clone命令后我们会默认处于 master 分支下，同时系统会自动将 origin 设置成该远程仓库的标识符。也就是说，当前本地仓库的 master 分支与 GitHub 端远程仓库（origin）的 master 分支在内容上是完全相同的。

```shell
git branch -a
```

我们用 git branch -a 命令查看当前分支的相关信息。添加 -a 参数可以同时显示本地仓库和远程仓库的分支信息。

### 获取远程指定分支

```shell
git checkout -b feature-D origin/feature-D
```

-b 参数的后面是本地仓库中新建分支的名称。为了便于理解，我们仍将其命名为 feature-D，让它与远程仓库的对应分支保持同名。新建分支名称后面是获取来源的分支名称。例子中指定了 origin/feature-D，就是说以名为 origin 的仓库（这里指 GitHub 端的仓库）的 feature-D 分支为来源，在本地仓库中创建 feature-D 分支。

## 获取最新的远程仓库分支

```shell
git pull origin feature-D
```

如果两人同时修改了同一部分的源代码，push 时就很容易发生冲突。所以多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作。

## 显示仓库远程地址

```shell
git config --get remote.origin.url
```
