---
title: "在 Python 中使用 Base64 编码和解码"
date: 2016/07/14 11:27
tags: [Base64]
categories: Python

---

## Base64 简介

Base64，简单地讲，就是用 64 个字符来表示二进制数据的方法，这 64 个字符包含小写字母 a-z、大写字母 A-Z、数字 0-9 以及符号"+"、"/"，其实还有一个 "=" 作为后缀用途，所以实际上有 65 个字符。

关于如何进行 Base64 编码转换的步骤可参考[此文](http://www.ruanyifeng.com/blog/2008/06/base64.html)。本文主要介绍如何使用 Python 进行 Base64 编码。事实上，Python 已经内置了一个用于 Base64 编解码的库：`base64`。编码使用 `base64.b64encode()` 方法，解码使用 `base64.b64decode()` 方法。

## 对文本进行 Base64 编码和解码

```python
>>> import base64
>>> str = 'hello world'
>>>
>>> base64_str = base64.b64encode(str)
>>> print base64_str
aGVsbG8gd29ybGQ=
>>>
>>> ori_str = base64.b64decode(base64_str)
>>> print ori_str
hello world
```

## 对图片进行 Base64 编码和解码

### 本地图片

```python
def convert_local_image():
    # 原始图片 ==> base64 编码
    with open('/path/to/alpha.png', 'r') as fin:
        image_data = fin.read()
        base64_data = base64.b64encode(image_data)

        fout = open('/path/to/base64_content.txt', 'w')
        fout.write(base64_data)
        fout.close()

    # base64 编码 ==> 原始图片
    with open('/path/to/base64_content.txt', 'r') as fin:
        base64_data = fin.read()
        ori_image_data = base64.b64decode(base64_data)

        fout = open('/path/to/beta.png', 'wb'):
        fout.write(ori_image_data)
        fout.close()
```

### 网络图片

```python
import requests

def convert_web_image():
    url = 'https://github.com/reactjs/redux/blob/master/logo/logo.png?raw=true'
    r = requests.get(url, stream=True)
    if r.status_code == 200:
        image_data = r.content
        base64_data = base64.b64encode(image_data)
        
        # 将图片的 base64 编码保存到本地文件
        with open('/path/to/base64_data.txt', 'w') as fout:
            fout.write(base64_data)
        
        # 下载图片到本地
        with open('/path/to/redux.png', 'wb') as fout:
            fout.write(image_data)
```


## 参考资料

- [Base64 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Base64)
- [Base64笔记 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2008/06/base64.html)

