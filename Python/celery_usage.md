# Celery

Celery 是一个异步任务的调度工具。它是 Python 写的库，但是它实现的通讯协议也可以使用 ruby，php，javascript 等调用。异步任务除了消息队列的后台执行的方式，还是一种则是跟进时间的计划任务。

使用 celery 包含三个方面，其一是定义任务函数，其二是运行celery服务，最后是客户应用程序的调用。

1. 定义任务函数：

```python
from celery import Celery

brokers = 'redis://127.0.0.1:6379/5'
backend = 'redis://127.0.0.1:6379/6'

app = Celery('tasks', broker=broker, backend=backend)

@app.task
def add(x, y):
    return x + y
```

上述代码导入了 celery，然后创建了 celery 实例 app，实例化的过程中，指定了任务名 tasks（和文件名一致），传入了 broker 和 backend。然后创建了一个任务函数add。

broker 是一个消息传输的中间件，可以理解为一个邮箱。每当应用程序调用 celery 的异步任务的时候，会向broker 传递消息，而后 celery 的 worker 将会取到消息，进行对于的程序执行。好吧，这个邮箱可以看成是一个消息队列。那么什么又是 backend，通常程序发送的消息，发完就完了，可能都不知道对方时候接受了。为此，celery 实现了一个 backend，用于存储这些消息以及 celery 执行的一些消息和结果。对于 brokers，官方推荐是 rabbitmq 和 redis，至于 backend，就是数据库啦。为了简单起见，我们都用 redis。


2. 启动 Celery 服务:

```
$ celery -A tasks worker --loglevel=info
```

上面的命令行实际上启动的是 Worker，如果要放到后台运行，可以扔给 supervisor。

3. 客户端程序调用，发送任务：

```
(env)$ python
>>> from tasks import add
>>> add.delay(4, 4)
```

上面是在 Python 环境中调用的 add 函数，实际上通常在应用程序中调用这个方法。

## 参考资料

- [使用celery之怎么让celery跑起来 - 小明明s à domicile](http://www.dongwm.com/archives/how-to-use-celery/)
- [异步任务神器 Celery 简明笔记 - 简书](http://www.jianshu.com/p/1840035cb510)
- [Celery快速入门 - Xiaoh写文字的地方 | Xiaoh's Blog](http://www.xiaoh.me/2015/12/17/celery-summary/)

