

当我们需要对多个变量同时初始化的时候，我们可能会采用下面的形式：

```python
a,b = True, False
```

但是当变量很多的时候，这种方式显得不是很优雅了：

```python
a,b,c,d,e,f = True, True, True, True, True, True
```

那么有什么优雅的方法呢，办法还是有的：

```
a,b,c,d,e,f = [True] * 6
a,b,c,d,e,f = (True,) * 6  // (d,) creates a one-item tuple, which is a sequence type
```

注意，上面的 `(True,)` 定义了一个值的元组。
 
## Reference

[python - More elegant way of declaring multiple variables at the same time - Stack Overflow](http://stackoverflow.com/questions/5495332/more-elegant-way-of-declaring-multiple-variables-at-the-same-time)

[Python和科学计算的帖子： - 哲思](http://www.zeuux.com/group/scipython/bbs/content/52019/)


## 删除字符串所有空格

- ''.join(str.split())
- 正则表达式


[python - How to strip all whitespace from string - Stack Overflow](http://stackoverflow.com/questions/3739909/how-to-strip-all-whitespace-from-string)





