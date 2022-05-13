---
date: 2022-05-02T18:39:29+08:00
author: "Rustle Karl"

title: "部署 Gitea"
url:  "posts/git/tools/gitea"  # 永久链接
tags: [ "git", "github", "gitlab" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

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

## 反向代理

> https://docs.gitea.io/zh-cn/reverse-proxies/

### 将 Nginx 作为反向代理服务并将 Gitea 路由至一个子路径

如果您已经有一个域名并且想与 Gitea 共享该域名，您可以增加以下 nginx.conf 配置中 server 的 http 部分，为 Gitea 添加路由规则：

```conf
server {
    listen 80;
    server_name git.example.com;

    # 注意: /git/ 最后需要有一个路径符号
    location /gitea/ { 
        # 注意: 反向代理后端 URL 的最后需要有一个路径符号
        proxy_pass http://localhost:3000/;
    }
}
```

然后必须在 Gitea 的配置文件中正确的添加类似 [server] ROOT_URL = http://git.example.com/gitea/ 的配置项。

### 将 Caddy 作为反向代理服务并将 Gitea 路由至一个子路径

```conf
git.example.com {
    # 注意: 路径 /git/ 最后需要有路径符号
    proxy /git/ http://localhost:3000
}
```
