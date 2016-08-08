---
title: "Python 的浅复制和深复制"
date: 2016/08/03 14:56
tags: [python]
categories: Python

---


- 浅复制
    如果对象（比如 list 或 dict）包含嵌套的对象（list 或 dict），列表中嵌套列表，就会导致对这些元素的操作是引用而不是复制。

- 深复制
    对象及其其中的元素都是彻彻底底的开辟新的内存空间进行复制。
    


用自身list[:]或dict.copy()方法实现浅复制，但是注意的是，虽然这两种办法能实现对象的复制，但是一旦对象包含的元素是可变的嵌套结构，如列表中嵌套列表，就会导致对这些元素的操作是引用而不是复制。也就是说，当我们改变原来对象某一元素里的数据时，其实经过这两种办法复制过来的对象也是随之改变的。

解决这种办法，需要实现真正的深复制，也就是说对象及其其中的元素都是彻彻底底的开辟新的内存空间进行复制。可以通过copy.deepcopy(list)或copy.deepcopy(dict)方法实现。

深复制也就是嵌套（递归）复制。


浅复制和深复制只针对复合对象而言，比如 list, dict, class


## 一些建议

- 如果对象中没有嵌套对象，可以考虑使用浅复制
- 如果对象中含有嵌套对象，为了真真正正开辟一块新的空间，应该使用 deepcopy


## 参考资料

- [Shallow and Deep Copy](http://www.python-course.eu/deep_copy.php)
- [What exactly is the difference between shallow copy, deepcopy and normal assignment operation? - Stack Overflow](http://stackoverflow.com/questions/17246693/what-exactly-is-the-difference-between-shallow-copy-deepcopy-and-normal-assignm)
- [Python基础-引用、浅复制、深复制的对比](http://www.lining0806.com/python%E5%9F%BA%E7%A1%80-%E5%BC%95%E7%94%A8%E3%80%81%E6%B5%85%E5%A4%8D%E5%88%B6%E3%80%81%E6%B7%B1%E5%A4%8D%E5%88%B6%E7%9A%84%E5%AF%B9%E6%AF%94/)


