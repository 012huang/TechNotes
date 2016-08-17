---
title: "快速搭建一个简单的 http 服务"
date: 2016/07/24 11:12
tags: [python]
categories: Python

---

## 搭建一个简单的 http 服务

利用 python 的 `SimpleHTTPServer`，我们可以使用下面的命令快速搭建一个简单的 http 服务：

```python
# 如果不填 port 的话，默认端口是 8000
$ python -m SimpleHTTPServer <port>
Serving HTTP on 0.0.0.0 port 8000 ...

# python3 的用法
$ python3 -m http.server <port>
```

在本机访问 http://localhost:8000，会列出该目录下的所有文件。假如该目录只有 index.html，则会显示 index.html 这个文件。

可以看到，上面的 HTTP 服务器服务的是网络中的所有主机（0.0.0.0），如果你只想让它在本地有效，可能你会这么尝试 `python -m SimpleHTTPServer 127.0.0.1:9000`，但这是不支持的。我们可以这么做：

<!--more-->

```python
import sys
from SimpleHTTPServer import SimpleHTTPRequestHandler
import BaseHTTPServer

def serve(HandlerClass=SimpleHTTPRequestHandler,
         ServerClass=BaseHTTPServer.HTTPServer):

    protocol = "HTTP/1.0"
    host = ''
    port = 8000
    if len(sys.argv) > 1:
        arg = sys.argv[1]
        if ':' in arg:
            host, port = arg.split(':')
            port = int(port)
        else:
            try:
                port = int(sys.argv[1])
            except:
                host = sys.argv[1]

    server_address = (host, port)

    HandlerClass.protocol_version = protocol
    httpd = ServerClass(server_address, HandlerClass)

    sa = httpd.socket.getsockname()
    print "Serving HTTP on", sa[0], "port", sa[1], "..."
    httpd.serve_forever()

if __name__ == "__main__":
    serve()
```

将上面的代码保存到文件 `server.py`，然后我们可以这么用：

```shell
$ python server.py 127.0.0.1     
Serving HTTP on 127.0.0.1 port 8000 ...

$ python server.py 127.0.0.1:9000
Serving HTTP on 127.0.0.1 port 9000 ...

$ python server.py 8080          
Serving HTTP on 0.0.0.0 port 8080 ...

```


## 在局域网共享资料

利用上面的 http 服务，我们可以简单地实现在局域网共享资料。假设在办公室有两台电脑 host1，host2，它们属于同个局域网，现在我们想将 host1 的某些文件共享给 host2，可以这么做：

- 进入到 host1 要共享的文件的目录，如果它们不在同一个目录，可以暂时将它们移到同一个目录
- 在该目录执行命令 `python -m SimpleHTTPServer`
- 使用 `ifconfig` 命令查看 host1 在局域网的 ip 地址，假设是 192.168.1.3
- 在 host2，打开浏览器，输入 `http://192.168.1.3:8000` 就可以查看到 host1 共享的文件了，然后就可以进行查看或下载了，就这么简单。


## 参考资料

- [SimpleHTTPServer: a quick way to serve a directory](http://www.2ality.com/2014/06/simple-http-server.html)

- [非常简单的Python HTTP 服务](http://coolshell.cn/articles/1480.html)

