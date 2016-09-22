#  装饰器

A decorator is a function that returns a function.

装饰器模式 Decorator 可以动态的扩充一个类或者函数的功能，实现的方法一般是在原有的类或者函数上包裹一层修饰类或修饰函数。

要理解Python的装饰器，就先要了解闭包。基本上支持函数式编程（函数可以作为对象传递）的语言，都支持闭包。我在之前Javascript闭包中曾介绍过它，Python的实现基本上也一样，就是在函数中返回其内部函数，这样当外部函数的生命周期结束后，其被内部函数使用的资源还会被保存下来。



```python
from functools import wraps

def logger(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        ts = time.time()
        result = fn(*args, **kwargs)
        te = time.time()
        print "function      = {0}".format(fn.__name__)
        print "    arguments = {0} {1}".format(args, kwargs)
        print "    return    = {0}".format(result)
        print "    time      = %.6f sec" % (te-ts)
        return result
    return wrapper
 
@logger
def multipy(x, y):
    return x * y

```

装饰器可以定义多个，调用顺序自下而上，也就是离函数定义最近的装饰器先被调用。

```python
def makebold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"

    return wrapped

def makeitalic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"

    return wrapped

@makebold        # 等同于 hello = makebold(makeitalic(hello))
@makeitalic      # 等同于 hello = makeitalic(hello)
def hello():
    return "hello world"
    
print hello()

# 结果
<b><i>hello world</i></b>
```

@makeitalic 装饰器将函数 hello 传递给函数 makeitalic，函数 makeitalic 执行完毕后返回被包装后的 hello 函数，而这个过程其实就是通过闭包实现的。@makebold 也是如此，只不过其传递的是 @makeitalic 装饰过的 hello 函数，因此最后的执行结果 `<b>` 在 `<i>` 外层，这个功能如果不用装饰器，其实就是显式的使用闭包：

```python
def makebold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"

    return wrapped

def makeitalic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"

    return wrapped

def hello():
    return "hello world"
    
hello = makeitalic(hello)
hello = makebold(hello)

print hello()

# 结果
<b><i>hello world</i></b>
```

```
# coroutine.py
#
# A decorator function that takes care of starting a coroutine
# automatically on call.

def coroutine(func):
    def start(*args,**kwargs):
        cr = func(*args,**kwargs)
        cr.next()
        return cr
    return start

# Example use
if __name__ == '__main__':
    @coroutine
    def grep(pattern):
        print "Looking for %s" % pattern
        while True:
            line = (yield)
            if pattern in line:
                print line,

    g = grep("python")
    # Notice how you don't need a next() call here
    g.send("Yeah, but no, but yeah, but no")
    g.send("A series of tubes")
    g.send("python generators rock!")
```

```
# grep.py
#
# A very simple coroutine

def grep(pattern):
    print "Looking for %s" % pattern
    while True:
        line = (yield)
        if pattern in line:
            print line,

# Example use
if __name__ == '__main__':
    g = grep("python")
    g.next()
    g.send("Yeah, but no, but yeah, but no")
    g.send("A series of tubes")
    g.send("python generators rock!")
```

```py
def max_age(*args):
    time.sleep(3)
    return max(args)

def cache_decorator(func):
    cache = {}
    def _wrapper(*args):
        if args in cache:
            return cache[args]
        cache[args] = result = func(*args)
        return result
    return _wrapper
cached_max_age = cache_decorator(max_age)
cached_max_age(1, 2, 3, 0)
cached_max_age(1, 2, 3, 0)
```


## 带参数的装饰器



## 装饰器的使用场景

从《Python高级编程》书上摘到，常见的装饰器使用场景有：

* 参数检查
* 缓存
* 代理
* 上下文提供者

## 参考资料

- [Python中的装饰器介绍 – 思诚之道](http://www.bjhee.com/python-decorator.html)
- [Python修饰器的函数式编程 - coolshell](http://coolshell.cn/articles/11265.html)
- [Python装饰器学习（九步入门）- cnblogs](http://www.cnblogs.com/rhcad/archive/2011/12/21/2295507.html)
- [Python 的闭包和装饰器 - SegmentFault](https://segmentfault.com/a/1190000004461404)
- [How can I make a chain of function decorators in Python? - Stack Overflow](http://stackoverflow.com/questions/739654/how-can-i-make-a-chain-of-function-decorators-in-python)
- [Python 设计模式: 装饰器模式(decorator pattern) - Mozillazg's Blog](https://mozillazg.com/2016/08/python-decorator-pattern.html)


