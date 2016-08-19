---
title: "Python 单元测试"
date: 2016/08/15 16:17
tags: []
categories: Python

---

# 单元测试


```python
import unittest

def fun(x):
    return x + 1

class MyTest(unittest.TestCase):
    def test(self):
        self.assertEqual(fun(3), 4)
        
if __name__ == '__main__':
    unittest.main()
```

