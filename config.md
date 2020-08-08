# Git 配置

## 设置别名

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
