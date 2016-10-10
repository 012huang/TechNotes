---
title: "Python 进阶"
date: 2016/10/08 16:55
tags: []
categories: 

---

# *args 和 **kwargs

并不是必须写成`*args`和`**kwargs`，只有变量前面的`*`才是必须的，你也可以写成`*var`和`**vars`，写成`*args`和`**kwargs`只是一个通俗的命名约定。

## *args 的用法

`*args` 和 `**kwargs` 主要用于函数定义。你可以将不定数量的参数传递给一个函数。

`*args` 是用来发送一个非键值对的可变数量的参数列表给一个函数.

```py
def test_var_args(f_arg, *argv):
    print("first normal arg:", f_arg)
    for arg in argv:
        print("another arg through *argv:", arg)

test_var_args('yasoob', 'python', 'eggs', 'test')
```

这会产生如下输出:

```
first normal arg: yasoob
another arg through *argv: python
another arg through *argv: eggs
another arg through *argv: test
```

## **kwargs 的用法

`**kwargs` 允许你将不定长度的**键值对**, 作为参数传递给一个函数。 如果你想要在一个函数里处理**带名字的参数**, 你应该使用`**kwargs`。

```python
def greet_me(**kwargs):
    for key, value in kwargs.items():
        print("{0} == {1}".format(key, value))


>>> greet_me(name="yasoob")
name == yasoob
```

## 使用 *args 和 **kwargs 来调用函数

现在有一个小函数：

```python
def test_args_kwargs(arg1, arg2, arg3):
    print("arg1:", arg1)
    print("arg2:", arg2)
    print("arg3:", arg3)
```

你可以使用`*args`或`**kwargs`来给这个小函数传递参数：

```python
# 首先使用 *args
>>> args = ("two", 3, 5)
>>> test_args_kwargs(*args)
arg1: two
arg2: 3
arg3: 5

# 现在使用 **kwargs:
>>> kwargs = {"arg3": 3, "arg2": "two", "arg1": 5}
>>> test_args_kwargs(**kwargs)
arg1: 5
arg2: two
arg3: 3
```

> 标准参数与`*args、**kwargs`在使用时的顺序

那么如果你想在函数里同时使用所有这三种参数， 顺序是这样的：

```
some_func(fargs, *args, **kwargs)
```

# 调试 (Debugging)

使用 Python debugger (pdb) 进行调试。

- 从命令行运行

在命令行使用Python debugger运行一个脚本， 举个例子：

```python
$ python -m pdb my_script.py
```

这会触发debugger在脚本第一行指令处停止执行。这在脚本很短时会很有帮助。你可以通过(Pdb)模式接着查看变量信息，并且逐行调试。

- 从脚本内部运行

你也可以在脚本内部设置断点，这样就可以在某些特定点查看变量信息和各种执行时信息了。这里将使用`pdb.set_trace()`方法来实现。举个例子：

```python
import pdb

def make_bread():
    pdb.set_trace()
    return "I don't have time"

print(make_bread())
```

保存上面的脚本后运行之，你会在运行时马上进入`debugger`模式。

## 命令列表

* `c`: 继续执行
* `w`: 显示当前正在执行的代码行的上下文信息
* `a`: 打印当前函数的参数列表
* `s`: 执行当前代码行，并停在第一个能停的地方（相当于单步进入）
* `n`: 继续执行到当前函数的下一行，或者当前行直接返回（单步跳过）

单步跳过（`n`ext）和单步进入（`s`tep）的区别在于， `单步进入`会进入当前行调用的函数内部并停在里面， 而`单步跳过`会（几乎）全速执行完当前行调用的函数，并停在当前函数的下一行。

# 生成器

首先我们要理解`迭代器(iterators)`。根据维基百科，迭代器是一个可以遍历一个容器（特别是列表）的对象。下面了解几个概念：

- 可迭代对象（Iterable）

Python中任意的对象，只要它定义了可以返回一个迭代器的`__iter__`方法，或者定义了可以支持下标索引的`__getitem__`方法(这些双下划线方法会在其他章节中全面解释)，那么它就是一个可迭代对象。简单说，==可迭代对象就是能提供迭代器的任意对象==。

- 迭代器（Iterator）

任意对象，只要定义了`next`(Python2) 或者`__next__`方法，它就是一个迭代器。

- 迭代（Iteration）

用简单的话讲，它就是从某个地方（比如一个列表）取出一个元素的过程。当我们使用一个循环来遍历某个东西时，这个过程本身就叫迭代。


**生成器也是一种迭代器，但是你只能对其迭代一次**。这是因为它们并没有把所有的值存在内存中，而是在运行时生成值。你通过遍历来使用它们，要么用一个“for”循环，要么将它们传递给任意可以进行迭代的函数和结构。大多数时候生成器是以函数来实现的。然而，它们并不返回一个值，而是`yield`(暂且译作“生出”)一个值。这里有个生成器函数的简单例子：

```py
def generator_function():
    for i in range(5):
        yield i

for item in generator_function():
    print(item)

# Output: 
# 0
# 1
# 2
# 3
# 4
```

==生成器最佳应用场景是：你不想同一时间将所有计算出来的大量结果集分配到内存当中，特别是结果集里还包含循环。==

下面是一个计算斐波那契数列的生成器：

```py
# generator version
def fibon(n):
    a = b = 1
    for i in range(n):
        yield a
        a, b = b, a + b
```

函数使用方法如下：

```
for x in fibon(1000000):
    print(x)
```

用这种方式，我们可以不用担心它会使用大量资源。

上面，我们说只能对生成器使用一次迭代。我们测试一下，在测试前你需要再知道一个Python内置函数：`next()`。它允许我们获取一个序列的下一个元素：

```py
def generator_function():
    for i in range(3):
        yield i

gen = generator_function()
print(next(gen))
# Output: 0
print(next(gen))
# Output: 1
print(next(gen))
# Output: 2
print(next(gen))
# Output: Traceback (most recent call last):
#            File "<stdin>", line 1, in <module>
#         StopIteration
```

我们可以看到，在`yield`掉所有的值后，`next()`触发了一个`StopIteration`的异常。基本上这个异常告诉我们，所有的值都已经被`yield`完了。你也许会奇怪，为什么我们在使用`for`循环时没有这个异常呢？啊哈，答案很简单。`for`循环会自动捕捉到这个异常并停止调用`next()`。

Python中一些内置数据类型也支持迭代：

```
my_string = "Yasoob"
next(my_string)
# Output: Traceback (most recent call last):
#      File "<stdin>", line 1, in <module>
#    TypeError: str object is not an iterator
```

好吧，这不是我们预期的。这个异常说那个str对象不是一个迭代器。对，就是这样！`它是一个可迭代对象，而不是一个迭代器`。这意味着它支持迭代，但我们不能直接对其进行迭代操作。那我们怎样才能对它实施迭代呢？是时候学习下另一个内置函数，iter。它将根据一个可迭代对象返回一个迭代器对象。这里是我们如何使用它：

```
my_string = "Yasoob"
my_iter = iter(my_string)
next(my_iter)
# Output: 'Y'
```

# Map, Filter 和 Reduce

## Map

`Map`会将一个函数映射到一个输入列表的所有元素上。这是它的规范：

**规范**

```
map(function_to_apply, list_of_inputs)
```

看一个例子：

```py
items = [1, 2, 3, 4, 5]
squared = []
for i in items:
    squared.append(i**2)
```

改用 Map 的方式：

```py
items = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, items))
# 上面加了list转换，是为了python2/3的兼容性
# 在python2中map直接返回列表，但在python3中返回迭代器
# 因此为了兼容python3, 需要list转换一下
```

上面我们使用 Map 将函数作用于 items 中的每个元素，这些元素是基本数据类型。事实上，我们可以将 items 的元素换成函数类型：

```python
def multiply(x):
        return (x*x)
def add(x):
        return (x+x)
items = [multiply, add]  # items 是一个函数列表，包含加法和乘法两个函数元素

for i in range(5):
    value = list(map(lambda x: x(i), items))
    print value

# Output:
# [0, 0]
# [1, 2]
# [4, 4]
# [9, 6]
# [16, 8]
```

## Reduce

当需要对一个列表进行一些计算并返回结果时，`Reduce` 是个非常有用的函数。

```
from functools import reduce
product = reduce( (lambda x, y: x * y), [1, 2, 3, 4] )

# Output: 24
```

## Filter

顾名思义，`filter`过滤列表中的元素，并且返回一个由所有符合要求的元素所构成的列表，`符合要求`即函数映射到该元素时返回值为True. 这里是一个简短的例子：

```
number_list = range(-5, 5)
less_than_zero = filter(lambda x: x < 0, number_list)
print(list(less_than_zero))  
# 上面print时，加了list转换，是为了python2/3的兼容性
# 在python2中filter直接返回列表，但在python3中返回迭代器
# 因此为了兼容python3, 需要list转换一下

# Output: [-5, -4, -3, -2, -1]
```

这个`filter`类似于一个`for`循环，但它是一个内置函数，并且更快。

# set (集合) 数据结构

























# 更多阅读

- [Python进阶](https://eastlakeside.gitbooks.io/interpy-zh/content/)
- [Intermediate Python](http://book.pythontips.com/en/latest/index.html)



