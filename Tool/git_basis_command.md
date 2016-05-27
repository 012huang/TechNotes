## 目录

<!-- MarkdownTOC -->

- [git 配置](#git-配置)
- [git 常用命令](#git-常用命令)
- [参考资料](#参考资料)

<!-- /MarkdownTOC -->


### git 配置

git 的全局配置文件在 `~/.gitconfig`，单个项目的配置文件在 `./.git/config`。

#### 全局配置

```shell
$ git config --global user.name my_name       # user.name
$ git config --global user.email my_email     # user.email
$ git config --global core.quotepath false    # 显示中文文件名
$ git config --global core.editor emacs       # 设置 Editor 为 emacs
$ git config --global alias.co checkout       # 设置别名
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.br branch
$ git config --list                           # 查看 git 的所有配置信息
```


#### 局部配置

有时我们需要在不同的项目使用不同的用户名和邮箱，因此最好给每个项目单独配置 `user.name` 和 `user.email`。

```shell
# 单独配置 user.name 和 user.email，--local 可以去掉
$ git config (--local) user.name another_name
$ git config (--local) user.email another_email
# 查看当前工作目录下的『用户名称』的配置
$ git config user.name 
```


### git 常用命令

#### 添加文件到暂存区

```shell
# 将某个文件修改提交到本地暂存区
$ git add <file>     
# 将所有修改过的工作文件提交暂存区  
$ git add .           
```

#### 查看项目状态

```shell
# 查看状态
$ git status

# 不要显示未跟踪的文件 
$ git status --untracked-files=no
$ git status -uno
```

#### 查看版本历史

- 查看当前项目的提交记录

```shell
# 详细
$ git log
# 简洁
$ git log --pretty=oneline
# 记录你的每一次命令
$ git reflog
```

- 查看某个文件的提交记录

```shell
$ git log path/to/file
```

#### 查看版本差异

- 查看当前项目修改前后的差异

```shell
$ git diff
```

- 查看单个文件修改前后的差异

```shell
$ git diff path/to/file
```

#### 版本回退

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
$ git checkout <commit hash> path/to/file
$ git reset <commit hash> path/to/file
```


#### 版本更新

- 更新某个文件

```shell
# 拉取远程仓库的更新数据
$ git fetch
# 检出最新版
$ git checkout origin/master -- path/to/file
```

#### 忽略已经跟踪的文件的改动

有时我们在本地修改了代码库中的配置文件，以便在本地运行，但不想让它提交到线上，可以使用以下的命令：

```shell
# 本地修改不提交到远程仓库
$ git update-index --assume-unchanged filename

# 取消本地忽略
$ git update-index --no-assume-unchanged 

# 查看本地仓库哪些文件被加入忽略列表
$ git ls-files -v
```
#### 忽略文件设置 (.gitignore, exclude)

默认情况下，`git` 目录下面的文件都会被上传到远程仓库，如果想忽略某些文件，比如编译生成的中间文件，日志文件等，这时可以在本地目录新建一个 `.gitignore` 文件，`.gitignore` 的用法可以参考下面这个链接:[A collection of useful .gitignore templates](https://github.com/github/gitignore)。

`git` 还提供了一种 `exclude` 的方式来忽略本地文件，与 `.gitignore` 不同的是，`.gitignore` 这个文件本身会被 push 到仓库中，它里面一般保存了公共的需要排除的文件，而 `exclude` 文件是自己本地忽略的设置，不会影响到其他人，也不会提交到仓库中。`exclude` 文件的位置在 `.git/info/exclude`，写法跟 `.gitignore` 类似。


#### 查看远程仓库

要查看当前配置有哪些远程仓库，可以用 `git remote -v` 命令，它会列出每个远程库的名字：

```shell
$ git remote -v
origin  git@github.com:ethan-funny/knowledge-lists.git (fetch)
origin  git@github.com:ethan-funny/knowledge-lists.git (push)
```

#### 查看分支

```shell
# 查看本地分支
$ git branch 
# 查看远程分支 
git branch -a 
```

### 参考资料

1. [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
2. [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
3. [Git 教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
4. [Git 常用命令备忘](http://stormzhang.com/git/2014/01/27/git-common-command/)


