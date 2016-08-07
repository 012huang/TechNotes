

# pip

## 安装 pip

在 mac 上使用 brew 安装 python，会附带安装 pip


## 安装 package

pip 支持从 [PyPI](http://pypi.python.org/pypi/) 、版本控制系统、本地项目, 甚至直接通过distribution文件安装package.

最常见的是使用 [Requirement Specifiers](http://pip-cn.readthedocs.org/en/latest/reference/pip_install.html#requirement-specifiers) 从 PyPI 安装。

```shell
$ pip install SomePackage            # 最新版本
$ pip install SomePackage==1.0.4     # 指定版本
$ pip install 'SomePackage>=1.0.4'     # 最低版本
```

## Requirements 文件

“Requirements 文件”中列出了需要安装的package，并可以通过 pip install 来安装:

```shell
$ pip install -r requirements.txt
```

这个文件的格式详情可以参考: [Requirements File Format](http://pip-cn.readthedocs.org/en/latest/reference/pip_install.html#requirements-file-format).


## python tips

- 查看某个包（module）的安装路径等信息

```shell
$ pip show module
$ python -c "import module; print module.__file__"
```

- 查看某个包的（module）的版本信息

```
$ pip show pymongo
```

- 查看所有可以更新的包

```
$ pip list -o
```

- 导入自定义的 package 要包含一个```__init__.py```的文件


## Reference

1. [pip 用户手册](http://pip-cn.readthedocs.org/en/latest/user_guide.html)


