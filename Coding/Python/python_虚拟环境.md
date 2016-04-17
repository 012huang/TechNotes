[Virtualenv](https://virtualenv.pypa.io/) 允许在一台机器上创建多个隔离的 `python` 运行环境，比如，有些项目是 `python 2.7` 的，有些项目却是 `python 3.1` 的，这时就需要创建两个独立的`python`运行环境了。[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/)提供了一些命令行的封装，更易于使用。


## 安装

```python
$ pip install virtualenv
$ pip install virtualenvwrapper
```

## virtualenv 的使用

### 创建虚拟环境

```python
# 创建一个名为 ENV 的虚拟环境，它会自动帮我们安装 python, pip 等
may@Matrix-MacBook-Pro:~[14:32] $ virtualenv ENV

New python executable in ENV/bin/python
Installing setuptools, pip, wheel...done.
```

### 进入虚拟环境

```python
may@Matrix-MacBook-Pro:~[14:38] $ cd ENV
may@Matrix-MacBook-Pro:ENV[14:38] $ source bin/activate

(ENV)may@Matrix-MacBook-Pro:ENV[14:38] $ python -V
Python 2.7.10
(ENV)may@Matrix-MacBook-Pro:ENV[14:39] $ pip list
pip (7.1.2)
setuptools (18.2)
wheel (0.24.0)

此时命令行前面会多出一个括号，这说明你已经进入名为 `ENV` 的虚拟环境了，以后 `easy_install` 或者 `pip` 安装的所有模块都会安装到该虚拟环境目录里。
```

### 退出虚拟环境

```python
# 退出当前虚拟环境
$ deactivate
```

## virtualenvwrapper 的使用

在使用 `virtualenvwrapper` 之前，我们需要先执行以下命令:

```shell
source /usr/local/bin/virtualenvwrapper.sh
```

为了避免每次都要手动执行，我们可以把它加入到 `.bashrc` 或 `.zshrc` 等。

### 创建并进入虚拟环境

```python
# 创建一个虚拟环境，默认的环境目录是 ~/.virtualenv/env1
# 创建完后，会自动进入到该虚拟环境
may@Matrix-MacBook-Pro:~ $ mkvirtualenv env1

New python executable in env1/bin/python
Installing setuptools, pip, wheel...done.
virtualenvwrapper.user_scripts creating /Users/imay/.virtualenvs/env1/bin/predeactivate
virtualenvwrapper.user_scripts creating /Users/imay/.virtualenvs/env1/bin/postdeactivate
virtualenvwrapper.user_scripts creating /Users/imay/.virtualenvs/env1/bin/preactivate
virtualenvwrapper.user_scripts creating /Users/imay/.virtualenvs/env1/bin/postactivate
virtualenvwrapper.user_scripts creating /Users/imay/.virtualenvs/env1/bin/get_env_details
(env1)imay@Matrix-MacBook-Pro:~ $
```

### 切换环境

`virtualenvwrapper` 提供了一个很方便的命令 `workon` 让我们切换虚拟环境，我们可以在任何地方使用 `workon`，而不用像 `virtualenv` 一样要进入环境的目录，然后再 `source` 一下。

```shell
$ workon [环境名]
```

### 退出环境

```shell
# 退出当前虚拟环境
$ deactive
```

### 删除环境

```shell
$ rmvirtualenv [环境名]
```

### 列出所有的虚拟环境

```shell
$ lsvirtualenv -b
```

## 参考资料
- [Virtualenvwrapper documentation](https://virtualenvwrapper.readthedocs.org/en/latest/)
- [Virtualenv documentation](https://virtualenv.pypa.io/en/latest/)

