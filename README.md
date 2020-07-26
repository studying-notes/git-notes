# Git 学习笔记

## 常用命令

| 命令 | 作用 |
| ---- | ---- |
| git status | 当前仓库的状态 |
| git add<file> | 暂存更改 |
| git reset HEAD<file> | 取消文件暂存更改 |
| git checkout <file> | 放弃文件更改 |
| git commit -m | 提交更改 |
| git commit --amend -m | 修正先前的提交 |
| git checkout <hash> | 切换旧版本、切换分支 |
|  |  |
| git tag <tag> | 打标签 |
| git tag -d<tag> | 移除标签 |
| git revert HEAD --no-edit | 撤销最后提交 |
| git reset --hard v1 | 从分支移除提交 |
| git mv <src dst> | 移动文件 |
| git checkout -b <branch> | 创建分支 |
| git branch -d <branch> | 删除分支 |
| git branch -D <branch> | 强制删除分支 |
| git branch -a | 列出全部分支 |
| git checkout -b <branch> <origin/branch> | 克隆远程分支 |
| git merge <branch> | 合并 |
| git rebase <branch> | 变基 |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |

### 显示提交历史

- `git log` - 项目提交历史

```shell
# 单行显示
git log --pretty=oneline

# 最大数量
git log --pretty=oneline --max-count=2

# 从几分钟前开始
git log --pretty=oneline --since='5 minutes ago'

# 到几分钟前结束
git log --pretty=oneline --until='5 minutes ago'

# 指定某人的提交记录
git log --pretty=oneline --author=<your name>

# 全部显示
git log --pretty=oneline --all
```

**自定义格式化**

- `--pretty="..."` 定义输出的格式
- `%h` 提交 HASH 的前几位
- `%d` 提交的分支头或标签
- `%ad` 创作日期
- `%s` 注释
- `%an` 作者姓名
- `--graph` 使用 ASCII 图形布局显示提交树
- `--date=short` 更短的日期形式

只看自己七天之内提交的更改：

```shell
git log --all --pretty=format:'%h %cd %s (%an)' --since='7 days ago'
```

不错的全部提交历史显示格式：

```shell
git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```

### 变基

`git merge dev`

```shell
> git hist
* f9b8c57 2020-07-26 | done (HEAD -> master) [Rustle Karl]
*   4717168 2020-07-26 | 冲突 [Rustle Karl]
|\
| * b89ee5b 2020-07-26 | m (dev) [Rustle Karl]
| * 0eecbca 2020-07-26 | ok [Rustle Karl]
* | 6cae58f 2020-07-26 | ok [Rustle Karl]
* | 1d547ea 2020-07-26 | ok [Rustle Karl]
|/
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]
```

将 master 中的更改集成到 dev 分支，用 rebase 命令代替 merge 命令来从 master 分支中引入更改。

`git rebase master`

```shell
> git checkout dev

> git hist
* b89ee5b 2020-07-26 | m (HEAD -> dev) [Rustle Karl]
* 0eecbca 2020-07-26 | ok [Rustle Karl]
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]

> git rebase master
Successfully rebased and updated refs/heads/dev.

> git hist
* 4a7b43a 2020-07-26 | done (HEAD -> dev, master) [Rustle Karl]
* f9b8c57 2020-07-26 | done [Rustle Karl]
*   4717168 2020-07-26 | 冲突 [Rustle Karl]
|\
| * b89ee5b 2020-07-26 | m [Rustle Karl]
| * 0eecbca 2020-07-26 | ok [Rustle Karl]
* | 6cae58f 2020-07-26 | ok [Rustle Karl]
* | 1d547ea 2020-07-26 | ok [Rustle Karl]
|/
* 6e886ea 2020-07-26 | inter [Rustle Karl]
* 523b3cb 2020-07-26 | init [Rustle Karl]
```

变基的最终结果与合并很相似。然而，提交树却十分不同。dev 分支的提交树已被重写，以致 master 分支成为了其提交历史的一部分。这使提交链更加线性，且更易阅读。

公开且与其他人共享的分支，重写公开的共享分支将会搞砸团队中的其他成员。

针对短期生命的本地分支使用变基，而对公开仓库的分支使用合并。


### 设置别名

添加下列内容到 `$HOME` 目录的 `.gitconfig` 文件中：

```ini
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```

```shell

```

```shell

```

```shell

```

