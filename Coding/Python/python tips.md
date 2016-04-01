
# python tips

- 查看某个包（module）的安装路径等信息

```shell
$ pip show module
$ python -c "import module; print module.__file__"
```

- 查看某个包的（module）的版本信息

```
$ pip show pymongo
```

- 导入自定义的 package 要包含一个```__init__.py```的文件

