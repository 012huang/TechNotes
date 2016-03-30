

# Python字符编码

## Python的默认字符集

Python的默认字符集在几个大版本中有过改变，以下是各个版本的默认字符集列举：

* Python2.1及以前： latin1
* Python2.3及之后，Python2.5以前：latin1 （但是会对非ASCII字符集字符提出WARNING）
* Python2.5及以后：ASCII
* Python3 : Unicode


## str & unicode
在python中,和字符串相关的类型,分别是str,unicode两种不同的类型,它们的父类是basestring,如图所示


```
# basestring，是str, unicode的父类
## str类型的字符串有多种编码方式，如ascii,gbk,utf8；而unicode字符串则没有这种说法
                                         +------+
                                     +-->| acsii|
                                     |   +------+
                                     |           
                                     |   +------+
                                     +-->| gbk  |
                       +---------+   |   +------+
                 +---->|   str   |---+           
                 |     +-+-----^-+   |           
                 |       |     |     |   +------+
                 |       |     |     +-->| utf8 |
+-----------+    |       |     |         +------+
|basestring |----+    decode  encode             
+-----------+    |       |     |                 
                 |       |     |                 
                 |     +-v-----+-+               
                 +---->| unicode |               
                       +---------+                       
```

## str & unicode互转

``` python
## str <-> unicode
str -> unicode (decode)
s.decode(encoding)

unicode -> str (encode)
u.encode(encoding)
```

```python
## 把一个gbk字符编码的str对象转换为utf-8的str对象
s = "你好" (假设是gbk编码)
# 把s转换成unicode，再从unicode转换成utf-8编码
s1 = s.decode('gbk')
s2 = s1.encode('utf-8')
# or s2 = s.decode('gbk').encode('utf-8')
```

## 例子

### example 1
```python
## 牢记:在进行同时包含 str 与 unicode 的运算时，Python 一律都把 str 转换成 unicode 再运算

# 正确，所有的字符串都是 str, 不需要 decode  
"中文：%s" % s   # 中文：关关雎鸠  
  
# 失败，相当于运行："中文：%s".decode('ascii') % u  
"中文：%s" % u  # UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 0: ordinal not in range(128)  
  
# 正确，所有字符串都是 unicode, 不需要 decode  
u"中文：%s" % u   # 中文：关关雎鸠  
  
# 失败，相当于运行：u"中文：%s" % s.decode('ascii')  
u"中文：%s" % s  # UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 0: ordinal not in range(128) 
```

### example2

```python

#!/usr/bin/python 
# -*- coding: utf8 -*-
# 使用utf8编码解释脚本文件

import sys

# 打印系统默认编码
print "system default encoding: " + sys.getdefaultencoding()

print '--------------'

# str字符串
s_str = '你好'
print(type(s_str))
print s_str
print s_str.decode('utf8') # s_str -> unicode

print '--------------'

# unicode字符串 
u_str = u'你好'
u_str2 = u'hello'
print(type(u_str))
print u_str.encode('utf-8')
print u_str2

# 相当于执行u_str.encode('ascii'),而unicode字符串含有非ascii的字符,因此出错
#print str(u_str)  

# raw_input只接收str类型字符串，不接收unicode类型，使用encode方法是为了将中文字符串(unicode)转成str类型
# 后面又加了decode是把name转为unicode类型
name = raw_input(u'请输入你的姓名：'.encode('utf-8')).decode('utf-8')
print u'%s你好，真是一个不错的名字，欢迎来到%s' %(name,u"法兰城")
print type(name)

d = {1:2, '1':'2', u'你好': 'hello'}
def key_in_dict(key):
    if key in d:
        return True
    return False

def key_found_in_dict(key):
    for _key in d:
        if _key == key:
            return True
    return False

print(key_in_dict(u'你好'))
print(key_found_in_dict(u'你好'))


# str + unicode
str1 = '123'
str2 = u'hello'

## str1 会先转为unicode类型
str3 = str1 + str2
print str3
print type(str3)
```

#### 结果

```python
system default encoding: ascii
--------------
<type 'str'>
你好
你好
--------------
<type 'unicode'>
你好
hello
请输入你的姓名：刘
刘你好，真是一个不错的名字，欢迎来到法兰城
<type 'unicode'>
True
True
123hello
<type 'unicode'>
```

### example3

看一个简单的小程序 hello.py

```python
hello = u'你好'
print hello
```

在终端执行 `python hello.py` 正常打印，但是如果将其重定向到文件 `python hello.py > result` 会发现 `UnicodeEncodeError`

这是因为：输出到控制台时，print 使用的是控制台的默认编码，而重定向到文件时，print 就不知道使用什么编码了，于是就使用了默认编码 ascii 导致出现编码错误。

应该改成如下:

```python
hello = u'你好'
print hello.encode('utf-8')
```

这样执行 `python hello.py > result` 就没有问题

## 字符编码笔记

### ASCII码

> 在计算机内部，所有的信息最终都表示为一个二进制的字符串。每一个二进制位（bit）有0和1两种状态，因此八个二进制位就可以组合出256种状态，这被称为一个字节（byte）。也就是说，一个字节一共可以用来表示256种不同的状态，每一个状态对应一个符号，就是256个符号，从0000000到11111111。

> 上个世纪60年代，美国制定了一套字符编码，对英语字符与二进制位之间的关系，做了统一规定。这被称为ASCII码，一直沿用至今。

> ASCII码一共规定了128个字符的编码，比如空格"SPACE"是32（二进制00100000），大写的字母A是65（二进制01000001）。这128个符号（包括32个不能打印出来的控制符号），只占用了一个字节的后面7位，最前面的1位统一规定为0。

举例，字符串bar的三个字母『b』『a』『r』对应的ASCII码分别为98、97和114，转换成二进制后分别为1100010，1100001和1110010。

#### 查询一个字符的ASCII码

```python

ascii -> char
$ python -c "print ord('a')"
$ printf "%d\n" "'a"
$ man ascii | grep -w 'a'

char -> ascii
$ python -c "print chr(97)"
$ awk -v char=97 'BEGIN { printf "%c\n", char; exit }'
```

### Unicode

> 世界上存在着多种编码方式，同一个二进制数字可以被解释成不同的符号。因此，要想打开一个文本文件，就必须知道它的编码方式，否则用错误的编码方式解读，就会出现乱码。为什么电子邮件常常出现乱码？就是因为发信人和收信人使用的编码方式不一样。

> 可以想象，如果有一种编码，将世界上所有的符号都纳入其中。每一个符号都给予一个独一无二的编码，那么乱码问题就会消失。这就是Unicode，就像它的名字都表示的，这是一种所有符号的编码。

> Unicode只是一个符号集，它只规定了符号的二进制代码，却没有规定这个二进制代码应该如何存储。
比如，汉字"严"的unicode是十六进制数4E25，转换成二进制数足足有15位（100111000100101），也就是说这个符号的表示至少需要2个字节。表示其他更大的符号，可能需要3个字节或者4个字节，甚至更多

### UTF-8

> UTF-8就是在互联网上使用最广的一种Unicode的实现方式。其他实现方式还包括UTF-16（字符用两个字节或四个字节表示）和UTF-32（字符用四个字节表示），不过在互联网上基本不用。重复一遍，这里的关系是，UTF-8是Unicode的实现方式之一


### 小结

> - 一个字节由8个二进制位组成
> - UTF-8是Unicode的实现方式之一;
> - ASCII编码是1个字节,而Unicode编码通常是2个字节及以上;
> - UTF-8最大的一个特点,就是它是一种可变长的编码方式.它可以使用1~4个字节表示一个符号,根据不同的符号而变化字节长度.


### 本节参考
[字符串和编码](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819196283586a37629844456ca7e5a7faa9b94ee8000)
[字符编码笔记](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)
[中日韩汉字Unicode编码表](http://www.chi2ko.com/tool/CJK.htm)
[字符集和字符编码](http://cenalulu.github.io/linux/character-encoding/)


## 最终建议
在Python中使用中文需要注意的点:

- Python2字符串的默认编码是'ASCII',Python3字符串的默认编码是'Unicode';
- 文件头加上 ```# -*- coding: utf-8 -*-```, 告诉Python解释器，按照UTF-8编码读取源代码;
- 文件头申明了UTF-8编码并不意味着你的.py文件就是UTF-8编码的，还要将其保存为UTF-8编码;
- 注意linux $LANG 环境变量(使用locale命令查看)和终端的字符编码要一致，最好都设置成UTF-8;
- 所有 text string 都应该是 unicode 类型，而不是 str;
- 在代码里的中文字符串前写上u，使得中文字符串是Unicode字符串，而不是str;

- str本身是不能encode的，如果想要encode，先要转化成unicode，此时采用默认的ascii进行转化;
- 在进行同时包含 str 与 unicode 的运算时，Python 一律都把 str 转换成 unicode 再运算，当然，运算结果也都是 unicode.由于 Python 事先并不知道 str 的编码，它只能使用 sys.getdefaultencoding() 编码去 decode,而sys.getdefaultencoding() 的值总是 'ascii',即默认编码是ascii;


## 参考文献
- [深入理解Python字符集编码](http://foofish.net/blog/16/understanding-python-charset)
- [python 字符编码与解码](http://blog.csdn.net/trochiluses/article/details/16825269)
- [Python的默认字符集](http://cenalulu.github.io/python/python-encoding/)
- [Python 的中文编码处理](http://in355hz.iteye.com/blog/1860787)
- [立即停止使用 setdefaultencoding('utf-8')](http://blog.ernest.me/post/python-setdefaultencoding-unicode-bytes?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)


