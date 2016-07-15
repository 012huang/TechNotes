---
title: "在 Python 中使用 socks 代理"
date: 2016-07-02 12:10:01
tags: [python]
categories: Python

---

# 简介

有时，我们可能需要在 python 代码中使用 socks 代理。比如，下面的代码如果不使用代理，可能无法正常工作：

```python
# -*- coding: utf-8 -*-

import urllib2

url = 'https://www.google.com/search?q=linux'
request = urllib2.Request(url)
request.add_header("User-Agent", "Mozilla/5.001 (windows; U; NT4.0; en-US; rv:1.0) Gecko/25250101")

html_source = urllib2.urlopen(request, timeout=10).read()

if html_source:
    print 'ok'
else:
    print 'fail'
```

在终端运行该代码，出现一个 `<urlopen error [Errno 65] No route to host` 的错误，也就是网络访问出错。

<!--more-->

为了能够正常访问，我们需要安装一个 pysocks 的包，它支持 socks 代理。现在，我们在上面的代码加上 socks 代理：

```python
# -*- coding: utf-8 -*-

import urllib2
import socket
import socks

SOCKS5_PROXY_HOST = '127.0.0.1' 
SOCKS5_PROXY_PORT = 1234  # socks 代理本地端口

default_socket = socket.socket 

socks.set_default_proxy(socks.SOCKS5, SOCKS5_PROXY_HOST, SOCKS5_PROXY_PORT) 
socket.socket = socks.socksocket

url = 'https://www.google.com/search?q=linux'
request = urllib2.Request(url)
request.add_header("User-Agent", "Mozilla/5.001 (windows; U; NT4.0; en-US; rv:1.0) Gecko/25250101")

html_source = urllib2.urlopen(request, timeout=10).read()

if html_source:
    print 'ok'
else:
    print 'fail'
```

重新运行，发现可以了。


# 参考资料
- [Using Python’s urllib2 or Requests with a SOCKS5 proxy](http://dae.me/blog/1959/using-pythons-urllib2-or-requests-with-a-socks5-proxy/)

