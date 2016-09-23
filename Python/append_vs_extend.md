---
title: "append vs. extend"
date: 2016/09/10 13:54
tags: [python]
categories: Python

---

# append vs extend

[`append`](https://docs.python.org/2/library/array.html?#array.array.append): Appends object at end.

```
x = [1, 2, 3]
x.append([4, 5])
print (x)
```

gives you: `[1, 2, 3, [4, 5]]`

* * *

[`extend`](https://docs.python.org/2/library/array.html?#array.array.extend): Extends list by appending elements from the iterable.

```
x = [1, 2, 3]
x.extend([4, 5])
print (x)
```

gives you: `[1, 2, 3, 4, 5]`

## another example

```
>>> a = [1, 2]
>>> a
[1, 2]
>>> a.append('hey')
[1, 2, 'hey']
>>> a.extend('hey')
>>> a
[1, 2, 'hey', 'h', 'e', 'y']
```

# 更多阅读

[python - append vs. extend - Stack Overflow](http://stackoverflow.com/questions/252703/append-vs-extend)



