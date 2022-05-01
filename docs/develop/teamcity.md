---
date: 2022-05-01T09:25:56+08:00
author: "Rustle Karl"

title: "TeamCity 持续集成软件部署"
url:  "posts/git/docs/develop/teamcity"  # 永久链接
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

echo "
## The address of the TeamCity server. The same as is used to open the TeamCity web interface in the browser.
## Must include the protocol specification (https:// is recommended).
serverUrl=http://localhost:8111/

## The unique name of the agent used to identify this agent on the TeamCity server
## Use blank name to let server generate it.
## By default, this name would be created from the build agent's host name
name=Default agent

## Container directory to create default checkout directories for the build configurations.
workDir=../work

## Container directory for the temporary directories.
## Please note that the directory may be cleaned between the builds.
tempDir=../temp

## Container directory for agent state files and caches.
## TeamCity agent assumes ownership of the directory and can delete the content inside.
systemDir=../system


######################################
#   Optional Agent Properties        #
######################################
## A token which is used to identify this agent on the TeamCity server for agent authorization purposes.
## It is automatically generated and saved back on the first agent connection to the server.
authorizationToken=1234567890abcdefghijklml
" > ~/bin/TeamCityAgent/conf/buildAgent.properties

~/bin/TeamCityAgent/bin/agent.sh start
```

### Docker

```
docker run -e SERVER_URL="<url to TeamCity server>"  \ 
    -v <path to agent config folder>:/data/teamcity_agent/conf  \      
    jetbrains/teamcity-agent
```

## 设置开机自启

```
~/bin/TeamCity/bin/teamcity-server.sh start
~/bin/TeamCityAgent/bin/agent.sh start
```
