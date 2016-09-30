# 闭包

## 什么是闭包

一个闭包就是你调用了一个函数 A，这个函数 A 返回了一个函数 B 给你。这个返回的函数 B 就叫做闭包。你在调用函数 A 的时候传递的参数就是自由变量。闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来。

事实上，我们常说的装饰器就是一种的闭包的应用，只不过其传递的是函数。

简单地说，函数中返回其内部函数，这样当外部函数的生命周期结束后，其被内部函数使用的资源还会被保存下来。个人觉得，闭包主要有两个作用：

1. 隐藏你要使用的对象，只有返回的内部函数才能访问它。这一点，在[Javascript闭包](http://www.bjhee.com/js-closure-iif.html)一文中已经提过。
2. 将拥有类似功能的函数统一实现，差异部分由传入的参数来区别，并通过内部函数来返回我们真正要用的函数。

父函数 func，子函数 inner_func

```python
def func(name):
    def inner_func(age):
        print 'name:', name, 'age:', age
    return inner_func

bb = func('the5fire')
bb(26)  # >>> name: the5fire age: 26
```

调用 func 的时候就产生了一个闭包——inner_func,并且该闭包持有自由变量——name，因此这也意味着，当函数func的生命周期结束之后，name这个变量依然存在，因为它被闭包引用了，所以不会被回收。

再看一个例子：

```py
def make_pow(n):
    def inner_func(x):
        return pow(x, n)
    return inner_func
    
pow2 = make_pow(2)
pow3 = make_pow(3)

pow2(4)  // 16
pow3(4)  // 64
```

## 闭包有什么用

闭包的最大特点是可以将父函数的变量与内部函数绑定，并返回绑定变量后的函数（也即闭包），此时即便生成闭包的环境（父函数）已经释放，闭包仍然存在，这个过程很像类（父函数）生成实例（闭包），不同的是父函数只在调用时执行，执行完毕后其环境就会释放，而类则在文件执行时创建，一般程序执行完毕后作用域才释放，因此对一些需要重用的功能且不足以定义为类的行为，使用闭包会比使用类占用更少的资源，且更轻巧灵活。现举一例：假设我们仅仅想打印出各类动物的叫声，分别以类和闭包来实现。

```
# 用类
class Animal():
    def __init__(self, animal):
        self.animal = animal
    
    def sound(self, voice):
        print self.animal, ':', voice, '...'

dog = Animal('dog')
dog.sound('wangwang')
dog.sound('wowo')

dog : wangwang ...
dog : wowo ...

# 用闭包
def voice(animal):
    def sound(voc):
        print animal, ':', voc, '...'
    return sound

dog = voice('dog')
dog('wangwang')
dog('wowo')
```

可以看到输出结果是完全一样的，但显然类的实现相对繁琐，且这里只是想输出一下动物的叫声，定义一个 Animal 类未免小题大做，而且 voice 函数在执行完毕后，其作用域就已经释放，但 Animal 类及其实例 dog 的相应属性却一直贮存在内存中


## js 中的闭包

```js
function count() {
    var i = 0;
    return function() {
        return ++i;
    }
}
```




## 参考资料

- [Python 的闭包和装饰器](https://segmentfault.com/a/1190000004461404)
- [Javascript闭包和立即执行函数的作用](http://www.bjhee.com/js-closure-iif.html)

