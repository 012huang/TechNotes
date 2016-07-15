
在介绍如何最简单地利用 `python` 实现并行前，我们先来看一个简单的代码。

```python
words = ['apple', 'bananan', 'cake', 'dumpling']
for word in words:
    print word
```

上面的例子中，我们用一个 `for` 循环打印出 `words` 列表中的每个单词。问题来了，这里我们打印完一个单词才能接着打印另一个单词，能不能同时打印呢？好比如在银行的营业厅排队，如果只开一个窗口办理业务，你需要等前面一个人办完，才轮到你，如果能开多个窗口，显然会快很多。

我们将上面的代码抽象成下面的模式：

```python
items = list()
for item in items:
    process(item)
```

其中，`items` 是一个列表，`process(arg)` 是一个函数，可以有返回值也可以没有。我们希望可以将这种模式改成并行处理的方式，比如可以引入多线程等处理方式，但是这些处理方式往往会让代码变得更加复杂。那么有什么简单的处理方式吗？我们将上面的模式进行下面的改造，使之可以并行处理：

```python
from multiprocessing.dummy import Pool as ThreadPool

items = list()

pool = ThreadPool()
pool.map(process, items)
pool.close()
pool.join()
```

下面我们进行测试：

```python
import time
from multiprocessing.dummy import Pool as ThreadPool

def get_logger(name):
    logger = logging.getLogger(name)
    logger.setLevel(logging.DEBUG)

    stream_handler = logging.StreamHandler()
    stream_handler.setLevel(logging.DEBUG)

    formatter = logging.Formatter(
        '%(asctime)s - %(name)s [%(levelname)s] %(message)s')

    stream_handler.setFormatter(formatter)
    logger.addHandler(stream_handler)

    return logger

def process(item):
    log = _get_logger(item)
    log.info("item: %s" % item)
    time.sleep(5)


items = ['apple', 'bananan', 'cake', 'dumpling']

pool = ThreadPool()
pool.map(process, items)
pool.close()
pool.join()
```

输出结果:

```
2016-06-07 11:23:57,530 - apple [INFO] word: apple
2016-06-07 11:23:57,530 - bananan [INFO] word: bananan
2016-06-07 11:23:57,530 - cake [INFO] word: cake
2016-06-07 11:23:57,531 - dumpling [INFO] word: dumpling
```

从上面显示的时间可以看到，我们已经由原来的串行打印变成并行打印了。

另外，上面的处理函数 `process` 是没有返回值的。假设 `process` 函数的返回值是 result，那么 `results = pool.map(process, items)` 的返回值是一个列表，每个元素对应着处理每个 `item` 的结果。

因此，

```python
results = list()

for item in item_list:
    result = process(item)
    results.append(result)

return results
```

上面的串行处理可以改成下面的并行处理：

```python
from multiprocessing.dummy import Pool as ThreadPool

pool = ThreadPool()
results = pool.map(process, item_list)
pool.close()
pool.join()

return results
```











