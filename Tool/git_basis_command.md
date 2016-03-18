

### 版本历史

- 查看当前项目的提交记录


```shell
# 详细
$ git log
# 简洁
$ git log --pretty=oneline
```

- 查看某个文件的提交记录

```shell
$ git log path/to/file
```


### 版本回退

在 `Git` 中，用 `HEAD` 表示当前版本，上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，
当然往上 10 个版本写成 `HEAD~10`。

- 将当前*项目*回退到上一个版本

```shell
$ git reset --hard HEAD^
```

- 将当前*项目*回退到某个版本

```shell
$ git reset --hard <commit hash>
```

- 取消在本地对某*文件*做的修改，将该*文件*还原到最近的版本

```shell
$ git checkout -- path/to/file
```

- 取消在本地对*文件*做的修改，将该*文件*还原到某个版本

```shell
git checkout <commit hash> path/to/file
```


### 版本更新

- 更新某个文件

```shell
# 下载远程仓库
$ git fetch
# 检出最新版
$ git checkout -- path/to/file
```


