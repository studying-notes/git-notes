---
date: 2022-05-02T18:39:29+08:00
author: "Rustle Karl"

title: "部署 Gitea 托管服务"
url:  "posts/git/tools/gitea"  # 永久链接
tags: [ "git", "gitea" ]
categories: [ "Git 学习笔记" ]

toc: true  # 目录
draft: false  # 草稿
---

## Docker 方式

```shell
docker pull gitea/gitea:1.16.6
```

```shell
docker run --restart=always -d --name gitea -p 10022:22 -p 13000:3000 -v /root/docker/gitea:/data -v /etc/timezone:/etc/timezone:ro -v /etc/localtime:/etc/localtime:ro gitea/gitea:1.16.6
```

### 访问日志

```shell
docker logs -f gitea
```

## 配置反向代理

> https://docs.gitea.io/zh-cn/reverse-proxies/

### Nginx

如果您已经有一个域名并且想与 Gitea 共享该域名，您可以增加以下 nginx.conf 配置中 server 的 http 部分，为 Gitea 添加路由规则：

```conf
server {
    listen 80;

    location /gitea/ { 
        proxy_pass http://localhost:3000/;
    }
}
```

然后必须在 Gitea 的配置文件中正确的添加类似 [server] ROOT_URL = http://git.example.com/gitea/ 的配置项。

### Caddy

```conf
git.example.com {
    proxy /git/ http://localhost:3000
}
```
