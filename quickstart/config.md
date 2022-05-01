---
date: 2020-07-14T16:20:00+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Git 与 GitHub 设置"  # 文章标题
description: "Git 多个账号设置、GitHub 通过 SSH 访问、设置别名等"
url:  "posts/git/quickstart/config"  # 设置网页链接，默认使用文件名
tags: [ "git", "github", "gitlab", "config" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---

## 网络代理

### 全局 Git 代理

```shell
git config --global http.proxy 'socks5://127.0.0.1:7890'
git config --global https.proxy 'socks5://127.0.0.1:7890'
```

### 仅 Github 代理

```shell
# socks5
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890

# http
git config --global http.https://github.com.proxy http://127.0.0.1:8118
```

### 取消代理

```shell
git config --global --unset http.https://github.com.proxy
```

## 单账号设置

```shell
git config --list
```

### 全局设置

```shell
git config --global user.name "Rustle Karl"
git config --global user.email "fu.jiawei@outlook.com"

# 换行符设置

# 默认 LF 换行符
git config --global core.eol lf

# 禁止自动转换 CRLF
git config --global core.autocrlf false

# 同时存在 CRLF 和 LF 则不允许提交
git config --global core.safecrlf true
```

### 局部设置

```shell
git config user.name "Rustle Karl"
git config user.email "fu.jiawei@outlook.com"
```

### 生成公钥

```shell
ssh-keygen -t rsa -C "fu.jiawei@outlook.com"
```

然后在网站上添加公钥：

```shell
cat ~/.ssh/id_rsa.pub
```

## `~/.ssh/config` 文件格式

```
Host 118.178.86.183
  HostName 118.178.86.183
  User root
  Port 13002
```

这个配置语法对于多账号共存应该特别重要。

## 多账号共存

1. 清除全局设置

```shell
git config --global --list
git config --global --unset user.name "Rustle Karl"
git config --global --unset user.email "fu.jiawei@outlook.com"
```

2. 生成不同网站的 SSH Keys，也可以相同

- Github

```shell
ssh-keygen -t rsa -f c:/users/admin/.ssh/id_rsa.github -C "fu.jiawei@outlook.com"
```

- Gitlab

```shell
ssh-keygen -t rsa -f c:/users/admin/.ssh/id_rsa.gitlab -C "fu.jiawei@outlook.com"
```

然后添加到对应的网站中。

3. 配置 `~/.ssh/config` 文件

```conf
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa.github

Host ubuntu-gitea
    HostName ubuntu
    Port 10022
    User git
    IdentityFile ~/.ssh/id_rsa.github

Host ubuntu
    HostName ubuntu
    Port 22
    User root
    IdentityFile ~/.ssh/id_rsa

Host slave
    HostName slave
    Port 22
    User root
    IdentityFile ~/.ssh/id_rsa
```

> git remote set-url origin ssh://git@ubuntu-gitea:10022/root/vbot.git

4. 验证是否成功

```shell
ssh -T git@github.com
```

```
Hi fujiawei-dev! You've successfully authenticated, but GitHub does not provide shell access.
```

```shell
ssh -T git@ubuntu-amd64-gitea -p10022
```

```
Hi there, root! You've successfully authenticated with the key named fu.jiawei@outlook.com, but Gitea does not provide shell access.
If this is unexpected, please log in with password and setup Gitea under another user.
```

## 设置别名

添加下列内容到 `$HOME` 目录的 `.gitconfig` 文件中：

```shell
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```
