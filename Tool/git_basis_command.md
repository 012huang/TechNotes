

### 查看版本历史

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

### 查看版本差异

- 查看当前项目修改前后的差异

```shell
$ git diff
```

- 查看单个文件修改前后的差异

```shell
$ git diff path/to/file
```


### 版本回退

在 `Git` 中，用 `HEAD` 表示当前版本，上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，
当前往上 10 个版本写成 `HEAD~10`。

- 将当前**项目**回退到上一个版本

```shell
$ git reset --hard HEAD^
```

- 将当前**项目**回退到某个版本

```shell
$ git reset --hard <commit hash>
```

- 取消在本地对某**文件**做的修改，将该**文件**还原到最近的版本

```shell
$ git checkout -- path/to/file
```

- 取消在本地对**文件**做的修改，将该**文件**还原到某个版本

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

### 忽略已经跟踪的文件的改动

有时我们在本地修改了代码库中的配置文件，以便在本地运行，但不想让它提交到线上，可以使用以下的命令：

```shell
# 本地修改不提交到远程仓库
git update-index --assume-unchanged filename

# 取消本地忽略
git update-index --no-assume-unchanged 

# 查看本地仓库哪些文件被加入忽略列表
git ls-files -v
```

### 查看远程仓库

要查看当前配置有哪些远程仓库，可以用 `git remote -v` 命令，它会列出每个远程库的名字：

```shell
$ git remote -v
origin  git@github.com:ethan-funny/knowledge-lists.git (fetch)
origin  git@github.com:ethan-funny/knowledge-lists.git (push)
```







