---
date: 2022-05-01T17:33:32+08:00
author: "Rustle Karl"

title: "部署 GitLab"
url:  "posts/git/tools/gitlab"  # 永久链接
tags: [ "git", "github", "gitlab" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

toc: true  # 目录
draft: false  # 草稿
---

## 拉取镜像

```shell
docker pull registry.gitlab.cn/omnibus/gitlab-jh:latest
```

## 启动镜像

```shell
export GITLAB_HOME=/root/docker/gitlab
```

```shell
sudo docker run --detach \
  --hostname ubuntu-amd64 \
  --publish 20443:443 --publish 20080:80 --publish 20022:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/config:/etc/gitlab \
  --volume $GITLAB_HOME/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/data:/var/opt/gitlab \
  --shm-size 256m \
  registry.gitlab.cn/omnibus/gitlab-jh:latest
```

```shell
sudo docker logs -f gitlab
```

默认密码在 docker/gitlab/config/initial_root_password 文件里。
