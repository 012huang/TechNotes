---
title: "在 Python 中使用 JSON"
date: 2016/07/16 17:58
tags: [python, json]
categories: Python

---

# JSON 简介

在介绍 JSON 之前，我们先介绍序列化（Serialization）和反序列化（Deserialization）的概念。

- 序列化： 将数据结构或对象转换成二进制串的过程。
- 反序列化：将在序列化过程中所生成的二进制串转换成数据结构或者对象的过程。

常见的序列化方法有：XML、JSON、Protobuf、Thrift 和 Avro 等。

[JSON](http://www.json.org/)（JavaScript Object Notation）是一种轻量级的网络数据交换格式，绝大部分编程语言都提供了很好的库来对 JSON 进行操作。键值对是 JSON 中最基本的数据结构。

Python 中已经内置了对 JSON 的支持，我们**把一个 Python 对象编码转换成 JSON 字符串称为 encoding，也就是序列化；把 JSON 字符串解码转换成 Python 对象称为 decoding，也就是反序列化**。

在 Python 中，常见的对象类型主要有：string, int, list, dict, tuple 等。

<!--more-->

## 将 Python 数据类型编码成 JSON 字符串

```python
>>> import json
>>> data1 = {'one': 1, 'two': 2, 'three': 3}
>>> data2 = {"one": 1, "tow": 2, "three": 3}
>>> data3 = [{'a':'A', 'b':(2, 3), 'c':6.0}]
>>>
>>> json.dumps(data1)
'{"three": 3, "two": 2, "one": 1}'
>>>
>>> json.dumps(data2)
'{"three": 3, "tow": 2, "one": 1}'
>>>
>>> json.dumps(data3)
'[{"a": "A", "c": 6.0, "b": [2, 3]}]'
>>>
>>> json.dumps(data3, sort_keys=True) # 按键排序
'[{"a": "A", "b": [2, 3], "c": 6.0}]'
```

## 将 JSON 字符串解码成 Python 数据类型

```python
>>> import json

>>> user_info= '{"name" : "john", "gender" : "male", "age": 28}'

>>> user_dict = json.loads(user_info)
>>> user_dict
{u'gender': u'male', u'age': 28, u'name': u'john'}
```

需要特别注意的是，JSON 字符串的键值应该是由双引号括起来的，否则就不算是 JSON 字符串，比如下面：

```python
>>> import json
>>> userinfo = "{'name' : 'john', 'gender' : 'male', 'age': 28}"

>>> json.loads(userinfo)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/Cellar/python/2.7.11/Frameworks/Python.framework/Versions/2.7/lib/python2.7/json/__init__.py", line 339, in loads
    return _default_decoder.decode(s)
  File "/usr/local/Cellar/python/2.7.11/Frameworks/Python.framework/Versions/2.7/lib/python2.7/json/decoder.py", line 364, in decode
    obj, end = self.raw_decode(s, idx=_w(s, 0).end())
  File "/usr/local/Cellar/python/2.7.11/Frameworks/Python.framework/Versions/2.7/lib/python2.7/json/decoder.py", line 380, in raw_decode
    obj, end = self.scan_once(s, idx)
ValueError: Expecting property name: line 1 column 2 (char 1)
```

上面出错的原因是字符串的键值是由单引号括起来的，不符合 JSON 的规范。如果你确实是想把上面的字符串转换成 Python 的字典类型，可以参考我之前写的另一篇文章: [将字符串转为字典](http://funhacks.net/2016/04/24/python_%E5%B0%86%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%BD%AC%E4%B8%BA%E5%AD%97%E5%85%B8/)。

```python
>>> import ast
>>> userinfo = "{'name' : 'john', 'gender' : 'male', 'age': 28}"

>>> ast.literal_eval(userinfo)
{'gender': 'male', 'age': 28, 'name': 'john'}
```

## 参考资料


- [序列化和反序列化](http://www.infoq.com/cn/articles/serialization-and-deserialization)
- [JSON对象 -- JavaScript 标准参考教程（alpha）](http://javascript.ruanyifeng.com/stdlib/json.html)
- [Python 处理 JSON](http://liuzhijun.iteye.com/blog/1859857)


