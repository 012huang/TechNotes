

# 数据类型

## size_t

- 在 C++ 中，设计 size_t 就是为了适应多个平台的。size_t
的引入增强了程序在不同平台上的可移植性。size_t 是针对系统定制的一种数据类型，一般是整型，因为 C/C++ 标准只定义一最低的位数，而不是必需的固定位数。而且在内存里，对数的高位对齐存储还是低位对齐存储各系统都不一样。为了提高代码的可移植性，就有必要定义这样的数据类型。一般这种类型都会定义到它具体占几位内存等。当然，有些是编译器或系统已经给定义好的。经测试发现，在 32 位系统中 size_t 是 4 字节的，而在 64 位系统中，size_t 是 8 字节的，这样利用该类型可以增强程序的可移植性

- sizt_t 是一种「整型」类型，里面保存的是一个整数，就像 int, long那样。这种整数用来记录一个大小(size)。size_t 的全称应该是 size type，就是说「一种用来记录大小的数据类型」

- 通常我们用 sizeof(XXX) 操作，这个操作所得到的结果就是 size_t 类型

- size_t 类型的数据其实是保存了一个整数，所以它也可以做加减乘除，也可以转化为 int 并赋值给 int 类型的变量

- size_t 是用 typedef 来实现的。你可能在某个头文件里面找到类似的语句：

```cpp
typedef unsigned int size_t
```

- 在标准 C/C++ 的语法中，只有int float char bool等基本的数据类型，至于 size_t,或 size_type 都是以后的编程人员为了方便记忆所定义的一些便于理解的由基本数据类型的变体类型。
例如：typedef int size_t; 定义了size_t为整型。
