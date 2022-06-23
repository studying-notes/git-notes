---
date: 2022-06-22T15:04:12+08:00
author: "Rustle Karl"

title: "submodule 子模块"
url:  "posts/git/docs/submodule"
tags: [ "Git", "README" ]
categories: [ "Git 学习笔记" ]

toc: true  # 目录
draft: false  # 草稿
---

> https://git-scm.com/book/zh/v2

> 因为主题的搜索功能依赖特定的目录名，所以手动改了目录名，之后怎么改 .gitmodules 文件都无法追踪改动，报错无法找到原来的目录，只能重新初始化父仓库了，强制推送。

Git 通过子模块来解决"一个项目在目录结构中包含另一个独立项目"这个问题。

子模块允许你将一个 Git 仓库作为另一个 Git 仓库的子目录。 它能让你将另一个仓库克隆到自己的项目中，同时还保持提交的独立。

## 添加子模块

```shell
git submodule add remote_url local_path
```

目录下产生一个 .gitmodules 文件，记录了模块映射。

当你不在那个目录中时，Git 并不会跟踪它的内容， 而是将它看作子模块仓库中的某个具体的提交。

### 提交改动

```shell
git push origin main
```

```shell

```
