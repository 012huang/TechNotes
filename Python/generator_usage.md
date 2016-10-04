# 生成器

在介绍生成器的概念之前，我们先来看一个任务：生成一个奇数数列 {1, 3, 5, 7, 9，...}。

```pyhton
def odd(n):
    i = 1
    L = []
    while i <= n:
        L.append(2 * i - 1)
        i++
    return L
```

为了精通 yield ,你必须要理解：当你调用这个函数的时候，函数内部的代码并不立马执行。




如果我们仅仅是需要拿到斐波那契序列的第 n 位，或者仅仅是希望依此产生斐波那契序列，那么上面这种传统方式就会比较耗费内存。

该函数在运行中占用的内存会随着参数 max 的增大而增大，如果要控制内存占用，最好不要用 List





任何包含 `yield` 语句的函数称为『生成器』，也就是说，生成器其实是一个函数，但这个函数比较特别，含有 yield 语句。

yield 的作用就是把一个函数变成一个 generator，带有 yield 的函数不再是一个普通函数，Python 解释器会将其视为一个 generator，调用 fab(5) 不会执行 fab 函数，而是返回一个 iterable 对象！在 for 循环执行时，每次循环都会执行 fab 函数内部的代码，执行到 yield b 时，fab 函数就返回一个迭代值，下次迭代时，代码从 yield b 的下一条语句继续执行，而函数的本地变量看起来和上次中断执行前是完全一样的，于是函数继续执行，直到再次遇到 yield。

一个带有 yield 的函数就是一个 generator，它和普通函数不同，生成一个 generator 看起来像函数调用，但不会执行任何函数代码，直到对其调用 next()（在 for 循环中会自动调用 next()）才开始执行。虽然执行流程仍按函数的流程执行，但每执行到一个 yield 语句就会中断，并返回一个迭代值，下次执行时从 yield 的下一个语句继续执行。看起来就好像一个函数在正常执行的过程中被 yield 中断了数次，每次中断都会通过 yield 返回当前的迭代值。


## 参考资料

- [Python yield 使用浅析](https://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/)
- [Function vs Generator in Python](http://code-maven.com/function-vs-generator-in-python)
- [Plain function or Callback - An example in Python](http://code-maven.com/function-or-callback-in-python)
- [Callback or Iterator in Python](http://code-maven.com/callback-or-iterator-in-python)
- [iterator - What does the "yield" keyword do in Python? - Stack Overflow](http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python)
- [谈谈Python的生成器 – 思诚之道](http://www.bjhee.com/python-yield.html)

To master `yield`, you must understand that **when you call the function, the code you have written in the function body does not run.** The function only returns the generator object, this is a bit tricky :-)

```
def foo():
    number = 0
    while True:
        val = yield number
        print 'hello', val
        if val:
            number = val
        else:
            number += 1

p = foo()
p.next()  
# 0
p.send(2)
# hello 2
# 2
p.next()
# hello None
# 3
```


