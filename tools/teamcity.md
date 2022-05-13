---
date: 2022-05-01T09:25:56+08:00
author: "Rustle Karl"

title: "TeamCity 持续集成软件部署"
url:  "posts/git/tools/teamcity"  # 永久链接
tags: [ "git", "github", "gitlab" ] # 自定义标签
series: [ "Git 学习笔记" ] # 文章主题/文章系列
categories: [ "学习笔记" ] # 文章分类

toc: true  # 目录
draft: false  # 草稿
---

## 下载软件

```shell
wget https://download.jetbrains.com/teamcity/TeamCity-2022.04.tar.gz
```

## 解压安装

```shell
mkdir ~/bin

tar -zxvf TeamCity-2022.04.tar.gz -C ~/bin
```

# 启动

貌似不能运行在 ARM 上。

```shell
~/bin/TeamCity/bin/teamcity-server.sh start
```

```shell
java -version
```

## 打开网址

http://ubuntu-amd64:8111/favorite/projects

## TeamCity Agent

### 原生安装

```shell
wget http://ubuntu-amd64:8111/update/buildAgentFull.zip
```

```shell
apt install p7zip-full -y

mkdir ~/bin/TeamCityAgent

7z x buildAgentFull.zip -o/root/bin/TeamCityAgent -aou

cd ~/bin/TeamCityAgent

# 修改服务主机的地址

~/bin/TeamCityAgent/bin/agent.sh start
```

### Docker

```
docker run -e SERVER_URL="<url to TeamCity server>"  \ 
    -v <path to agent config folder>:/data/teamcity_agent/conf  \      
    jetbrains/teamcity-agent
```

## 反向代理设置

> https://www.jetbrains.com/help/teamcity/configuring-proxy-server.html

### 设置路径上下文

```
TEAM_CITY_PATH=/root/bin/TeamCity
mv $TEAM_CITY_PATH/webapps/ROOT $TEAM_CITY_PATH/webapps/teamcity 
```

## 设置开机自启

```
~/bin/TeamCity/bin/teamcity-server.sh start
~/bin/TeamCity/bin/teamcity-server.sh stop

~/bin/TeamCityAgent/bin/agent.sh start
~/bin/TeamCityAgent/bin/agent.sh stop
```
