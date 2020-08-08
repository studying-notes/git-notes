# 显示提交历史

> `git log` - 显示项目提交历史

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

## 自定义格式化

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
