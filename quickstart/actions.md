---
date: 2022-01-29T12:48:15+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "GitHub Actions 基础介绍"  # 文章标题
# description: "文章描述"
url:  "posts/git/quickstart/actions"  # 设置网页永久链接
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

## 前言

Github Actions 是 GitHub 推出的持续集成 (Continuous integration，简称 CI) 服务，它提供了配置非常不错的虚拟服务器环境，基于它可以进行构建、测试、打包、部署项目。简单来讲就是将软件开发中的一些流程交给云服务器自动化处理，比方说开发者把代码 push 到 GitHub 后它会自动测试、编译、发布。

## 基础概念

- **workflow** （工作流程）：持续集成一次运行的过程。
- **job** （任务）：一个 workflow 由一个或多个 job 构成，含义是一次持续集成的运行，可以完成多个任务。
- **step**（步骤）：每个 job 由多个 step 构成，一步步完成。
- **action** （动作）：每个 step 可以依次执行一个或多个命令（action）。

## 虚拟环境

GitHub Actions 为每个任务 (job) 都提供了一个虚拟机来执行，每台虚拟机都有相同的硬件资源：

- 2-core CPU
- 7 GB RAM 内存
- 14 GB SSD 硬盘空间

> 实测硬盘总容量为90G左右，可用空间为30G左右。

使用限制：

- 每个仓库只能同时支持 20 个 workflow 并行。
- 每小时可以调用 1000 次 GitHub API。
- 每个 job 最多可以执行 6 个小时。
- 免费版的用户最大支持 20 个 job 并发执行，macOS 最大只支持 5 个。
- 私有仓库每月累计使用时间为 2000 分钟，超过后 $0.008/ 分钟，公共仓库则无限制。

操作系统方面可选择 Windows Server、Linux、macOS，并预装了大量软件包和工具。

> **TIPS：** 虽然名称叫持续集成，但当所有任务终止和完成时，虚拟环境内的数据会随之清空，并不会持续。即每个新任务都是一个全新的虚拟环境。

## workflow 文件

GitHub Actions 的配置文件叫做 workflow 文件（官方中文翻译为“工作流程文件”），存放在代码仓库的 `.github/workflows` 目录中。workflow 文件采用 YAML 格式，文件名可以任意取，但是后缀名统一为 `.yml`，比如 `p3terx.yml`。一个库可以有多个 workflow 文件，GitHub 只要发现 `.github/workflows` 目录里面有 `.yml` 文件，就会按照文件中所指定的触发条件在符合条件时自动运行该文件中的工作流程。在 Actions 页面可以看到很多种语言的 workflow 文件的模版，可以用于简单的构建与测试。

下面是一个简单的 workflow 文件示例：

```yaml
name: Hello World
on: push
jobs:
  my_first_job:
    name: My first job
    runs-on: ubuntu-latest
    steps:
    - name: checkout
      uses: actions/checkout@master
    - name: Run a single-line script
      run: echo "Hello World!"
  my_second_job:
    name: My second job
    runs-on: macos-latest
    steps:
    - name: Run a multi-line script
      env:
        MY_VAR: Hello World!
        MY_NAME: P3TERX
      run:
        echo $MY_VAR
        echo My name is $MY_NAME
```

## workflow 语法

> **TIPS：** 参照上面的示例阅读。

### name

`name` 字段是 workflow 的名称。若忽略此字段，则默认会设置为 workflow 文件名。

### on

`on` 字段指定 workflow 的触发条件，通常是某些事件，比如示例中的触发事件是 `push`，即在代码 `push` 到仓库后被触发。`on` 字段也可以是事件的数组，多种事件触发，比如在 `push` 或 `pull_request` 时触发：

```yaml
on: [push, pull_request]
```

完整的事件列表，请查看官方文档。下面是一些比较常见的事件：

push 指定分支触发

```yaml
on:
  push:
    branches:
      - master
```

push tag 时触发

```yaml
on:
  push:
    tags:
    - 'v*'
```

定时触发

```yaml
schedule:
  - cron: 0 */6 * * *
```

发布 release 触发

```yaml
on:
  release:
    types: [published]
```

仓库被 star 时触发

```yaml
on:
  watch:
    types: [started]
```

### jobs

`jobs` 表示要执行的一项或多项任务。每一项任务必须关联一个 ID (`job_id`)，比如示例中的 `my_first_job` 和 `my_second_job`。`job_id` 里面的 `name` 字段是任务的名称。`job_id` 不能有空格，只能使用数字、英文字母和 `-` 或`_`符号，而 `name` 可以随意，若忽略 `name` 字段，则默认会设置为 `job_id`。

当有多个任务时，可以指定任务的依赖关系，即运行顺序，否则是同时运行。

```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

上面代码中，`job1` 必须先于 `job2` 完成，而 `job3` 等待 `job1` 和 `job2` 的完成才能运行。因此，这个 workflow 的运行顺序依次为：`job1`、`job2`、`job3`。

### runs-on

`runs-on` 字段指定任务运行所需要的虚拟服务器环境，是必填字段，目前可用的虚拟机如下：

> **TIPS：** 每个任务的虚拟环境都是独立的。

| 虚拟环境               | YAML workflow 标签                |
| :--------------------- | :-------------------------------- |
| Windows Server 2019    | `windows-latest`                  |
| Ubuntu 18.04           | `ubuntu-latest` or `ubuntu-18.04` |
| Ubuntu 16.04           | `ubuntu-16.04`                    |
| macOS X Catalina 10.15 | `macos-latest`                    |

### steps

`steps` 字段指定每个任务的运行步骤，可以包含一个或多个步骤。步骤开头使用 `-` 符号。每个步骤可以指定以下字段:

- `name`：步骤名称。
- `uses`：该步骤引用的`action`或 Docker 镜像。
- `run`：该步骤运行的 bash 命令。
- `env`：该步骤所需的环境变量。

其中 `uses` 和 `run` 是必填字段，每个步骤只能有其一。同样名称也是可以忽略的。

## action

`action` 是 GitHub Actions 中的重要组成部分，这点从名称中就可以看出，`actions` 是 `action` 的复数形式。它是已经编写好的步骤脚本，存放在 GitHub 仓库中。

对于初学者来说可以直接引用其它开发者已经写好的 `action`，可以在官方 action 仓库或者 GitHub Marketplace 去获取。此外 Awesome Actions 这个项目收集了很多非常不错的 `action`。

既然 `action` 是代码仓库，当然就有版本的概念。引用某个具体版本的 `action`：

```yaml
steps:
  - uses: actions/setup-node@74bc508 
# 指定一个 commit
  - uses: actions/setup-node@v1.2    
# 指定一个 tag
  - uses: actions/setup-node@master  
# 指定一个分支
```

一般来说 `action` 的开发者会说明建议使用的版本。
