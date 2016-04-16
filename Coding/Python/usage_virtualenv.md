
## 安装

```python
$ pip install virtualenv
```

## 创建虚拟环境

```python
maygou@Matrix-MacBook-Pro:~[14:32] $ virtualenv ENV
New python executable in ENV/bin/python
Installing setuptools, pip, wheel...done.
```

## 激活虚拟环境

```python
maygou@Matrix-MacBook-Pro:~[14:38] $ cd ENV
maygou@Matrix-MacBook-Pro:ENV[14:38] $ source bin/activate
(ENV)maygou@Matrix-MacBook-Pro:ENV[14:38] $ python -V
Python 2.7.10
(ENV)maygou@Matrix-MacBook-Pro:ENV[14:39] $ pip list
pip (7.1.2)
setuptools (18.2)
wheel (0.24.0)

此时命令行前面会多出一个括号，这说明你已经进入名为 `ENV` 的虚拟环境了，以后 `easy_install` 或者 `pip` 安装的所有模块都会安装到该虚拟环境目录里。
```


## 退出虚拟环境

```
deactivate
```


