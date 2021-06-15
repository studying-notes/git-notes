---
date: 2021-01-06T01:40:44+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "Gitea 配置文件"  # 文章标题
# description: "文章描述"
url:  "posts/git/addition/gitea"  # 设置网页永久链接
tags: [ "git", "gitea"]  # 标签
series: [ "Git 学习笔记"] # 文章主题/文章系列
categories: [ "学习笔记"] # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

```ini
APP_NAME = Gitea: Git with a cup of tea
RUN_MODE = prod
RUN_USER = git

[repository]
ROOT = /data/git/repositories

[repository.local]
LOCAL_COPY_PATH = /data/gitea/tmp/local-repo

[repository.upload]
TEMP_PATH = /data/gitea/uploads

[server]
APP_DATA_PATH    = /data/gitea
DOMAIN           = 192.168.199.208
SSH_DOMAIN       = 192.168.199.208
HTTP_PORT        = 3000
ROOT_URL         = http://192.168.199.208:13000/
DISABLE_SSH      = false
SSH_PORT         = 10022
SSH_LISTEN_PORT  = 22
LFS_START_SERVER = true
LFS_CONTENT_PATH = /data/git/lfs
LFS_JWT_SECRET   = OgQZYs9EpnbSNHwm92rIrbDRwQGNtwNcTInnu7X9CdY
OFFLINE_MODE     = false

[database]
PATH     = /data/gitea/gitea.db
DB_TYPE  = sqlite3
HOST     = localhost:3306
NAME     = gitea
USER     = root
PASSWD   = 
LOG_SQL  = false
SCHEMA   = 
SSL_MODE = disable
CHARSET  = utf8

[indexer]
ISSUE_INDEXER_PATH = /data/gitea/indexers/issues.bleve

[session]
PROVIDER_CONFIG = /data/gitea/sessions
PROVIDER        = file

[picture]
AVATAR_UPLOAD_PATH            = /data/gitea/avatars
REPOSITORY_AVATAR_UPLOAD_PATH = /data/gitea/repo-avatars
DISABLE_GRAVATAR              = true
ENABLE_FEDERATED_AVATAR       = false

[attachment]
PATH = /data/gitea/attachments

[log]
MODE                 = console
LEVEL                = info
REDIRECT_MACARON_LOG = true
MACARON              = console
ROUTER               = console
ROOT_PATH            = /data/gitea/log

[security]
INSTALL_LOCK   = true
SECRET_KEY     = 0aAm8XkQCnLMQ7iZY3fRh85Q4zJQITUvZKBB5UQIzO2VHrCnWRl4r0dtWlfnTkQ0
INTERNAL_TOKEN = eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYmYiOjE2MDk3NTg0MjJ9.9-tWTH5nwZaV6d3PQTU3EGa86TPdJLwF81xrkMK9S6M

[service]
DISABLE_REGISTRATION              = false
REQUIRE_SIGNIN_VIEW               = false
REGISTER_EMAIL_CONFIRM            = false
ENABLE_NOTIFY_MAIL                = false
ALLOW_ONLY_EXTERNAL_REGISTRATION  = false
ENABLE_CAPTCHA                    = false
DEFAULT_KEEP_EMAIL_PRIVATE        = false
DEFAULT_ALLOW_CREATE_ORGANIZATION = true
DEFAULT_ENABLE_TIMETRACKING       = true
NO_REPLY_ADDRESS                  = noreply.localhost

[oauth2]
JWT_SECRET = NDtl5TywPgATskw71xQFcNichmtbgYHSiOD94JmH370

[mailer]
ENABLED = false

[openid]
ENABLE_OPENID_SIGNIN = true
ENABLE_OPENID_SIGNUP = true

[cron]
ENABLED = true
RUN_AT_START = true

[cron.update_mirrors]
SCHEDULE = @every 24h

[other]
SHOW_FOOTER_BRANDING = false
SHOW_FOOTER_VERSION = false
SHOW_FOOTER_TEMPLATE_LOAD_TIME = false
```
