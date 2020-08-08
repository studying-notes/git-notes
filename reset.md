# 撤销提交

```shell
$ git add README.md
$ git commit -m "init"
```

现在撤销上一步提交操作：

```shell
$ git reset --soft HEAD^
```

这只是撤销上一步的 `commit` 操作，代码更改仍然保留。

`HEAD^` 表示上一次 `commit` 操作，如果想撤销两次 `commit` 操作，可以改为 `HEAD~2`。

## 参数

- `--mixed` - 不删除工作空间改动代码，撤销 `commit`，并且撤销 `git add .` 操作，默认参数
- `--soft  ` - 不删除工作空间改动代码，撤销 `commit`，不撤销 `git add .`
- `--hard` - 删除工作空间改动代码，撤销 `commit`，撤销 `git add .`
