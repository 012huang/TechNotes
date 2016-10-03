---
title: "Python 模块导入方法"
date: 2016/09/28 10:24
tags: [python]
categories: Python

---

# Python 模块导入方法

- 主程序与模块程序在同一目录下

如下面程序结构：

```
`-- src   
    |-- mod1.py   
    `-- test1.py
```

若在程序 test1.py 中导入模块 mod1，则直接使用 `import mod1` 或 `from mod1 import *`。

- 主程序所在目录是模块所在目录的父目录

如下面程序结构：

```
`-- src   
    |-- mod1.py   
    |-- mod2   
    |   `-- mod2.py   
    `-- test1.py
```

若在程序 test1.py 中导入模块 mod2，需要在 mod2 文件夹中建立空文件 `__init__.py` 文件（也可以在该文件中自定义输出模块接口），然后使用 `from mod2.mod2 import *` 或 `import mod2.mod2`。

- 主程序导入上层目录中模块或其他目录（平级）下的模块

如下面程序结构：

```
`-- src   
    |-- mod1.py   
    |-- mod2   
    |   `-- mod2.py   
    |-- sub   
    |   `-- test2.py   
    `-- test1.py  
```

若在程序 test2.py 中导入模块 mod1 和 mod2。首先需要在 mod2 下建立 `__init__.py` 文件(同2)，src下不必建立该文件。然后调用方式如下:

下面程序执行方式均在程序文件所在目录下执行，如 test2.py 是在 cd sub;之后执行 `python test2.py`

而 test1.py 是在 cd src;之后执行 `python test1.py`; 不保证在 src 目录下执行 `python sub/test2.py` 成功。

```
$ cat test2.py

import sys   
sys.path.append("..")   
import mod1   
import mod2.mod2
```


# 参考资料

- [详解Python模块导入方法 - 51CTO.COM](http://mobile.51cto.com/symbian-272844.htm)

