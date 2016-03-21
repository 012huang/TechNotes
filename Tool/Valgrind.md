
<!-- MarkdownTOC -->

- [Valgrind 介绍](#valgrind-介绍)
- [Valgrind的主要功能](#valgrind的主要功能)
- [Valgrind 安装](#valgrind-安装)
- [Valgrind 使用](#valgrind-使用)
- [Valgrind 使用举例](#valgrind-使用举例)
- [Reference](#reference)

<!-- /MarkdownTOC -->

## Valgrind 介绍 

Valgrind 是一个GPL的软件，用于Linux（For x86, amd64 and ppc32）程序的内存调试和代码剖析。你可以在它的环境中运行你的程序来监视内存的使用情况，比如C 语言中的malloc和free或者 C++中的new和 delete。使用Valgrind的工具包，你可以自动的检测许多内存管理和线程的bug，避免花费太多的时间在bug寻找上，使得你的程序更加稳固。

## Valgrind的主要功能

Valgrind工具包包含多个工具：

- Memcheck。这是 valgrind 应用最广泛的工具，一个重量级的内存检查器，能够发现开发中绝大多数内存错误使用情况，比如：使用未初始化的内存，使用已经释放了的内存，内存访问越界等。这也是本文将重点介绍的部分。
- Callgrind。它主要用来检查程序中函数调用过程中出现的问题。
- Cachegrind。它主要用来检查程序中缓存使用出现的问题。
- Helgrind。它主要用来检查多线程程序中出现的竞争问题。
- Massif。它主要用来检查程序中堆栈使用中出现的问题。
- Extension。可以利用 core 提供的功能，自己编写特定的内存调试工具。


下面分别介绍个工具的作用：

Memcheck 工具主要检查下面的程序错误：
  * 使用未初始化的内存 (Use of uninitialised memory) 
  * 使用已经释放了的内存 (Reading/writing memory after it has been free'd) 
  * 使用超过 malloc分配的内存空间(Reading/writing off the end of malloc'd blocks) 
  * 对堆栈的非法访问 (Reading/writing inappropriate areas on the stack) 
  * 申请的空间是否有释放 (Memory leaks -- where pointers to malloc'd blocks are lost forever) 
  * malloc/free/new/delete申请和释放内存的匹配(Mismatched use of malloc/new/new [] vs free/delete/delete []) 
  * src和dst的重叠(Overlapping src and dst pointers in memcpy() and related functions) 

==== Callgrind ====

Callgrind收集程序运行时的一些数据，函数调用关系等信息，还可以有选择地进行cache 模拟。在运行结束时，它会把分析数据写入一个文件。callgrind_annotate可以把这个文件的内容转化成可读的形式。

==== Cachegrind ====

它模拟 CPU中的一级缓存I1,D1和L2二级缓存，能够精确地指出程序中 cache的丢失和命中。如果需要，它还能够为我们提供cache丢失次数，内存引用次数，以及每行代码，每个函数，每个模块，整个程序产生的指令数。这对优化程序有很大的帮助。

==== Helgrind ====

它主要用来检查多线程程序中出现的竞争问题。Helgrind 寻找内存中被多个线程访问，而又没有一贯加锁的区域，这些区域往往是线程之间失去同步的地方，而且会导致难以发掘的错误。Helgrind实现了名为"Eraser" 的竞争检测算法，并做了进一步改进，减少了报告错误的次数。

==== Massif ====

堆栈分析器，它能测量程序在堆栈中使用了多少内存，告诉我们堆块，堆管理块和栈的大小。Massif能帮助我们减少内存的使用，在带有虚拟内存的现代系统中，它还能够加速我们程序的运行，减少程序停留在交换区中的几率。

 
## Valgrind 安装

  1、    到www.valgrind.org下载最新版valgrind-3.2.3.tar.bz2
  2、    解压安装包：tar –jxvf valgrind-3.2.3.tar.bz2
  3、    解压后生成目录valgrind-3.2.3 
  4、    cd valgrind-3.2.3
  5、    ./configure
  6、    Make;make install

## Valgrind 使用

用法: valgrind [options] prog-and-args
[options]:
常用选项，适用于所有Valgrind工具
  --tool=<name>     最常用的选项。运行 valgrind中名为toolname的工具。默认memcheck。
  -h --help                 显示帮助信息。
  --version                 显示valgrind内核的版本，每个工具都有各自的版本。
  -q --quiet                    安静地运行，只打印错误信息。
  -v --verbose              更详细的信息, 增加错误数统计。
  --trace-children=no|yes   跟踪子线程? [no]
  --track-fds=no|yes        跟踪打开的文件描述？[no]
  --time-stamp=no|yes       增加时间戳到LOG信息? [no]
  --log-fd=<number>     输出LOG到描述符文件 [2=stderr]
  --log-file=<file>     将输出的信息写入到filename.PID的文件里，PID是运行程序的进行ID
  --log-file-exactly=<file>     输出LOG信息到 file
  --log-file-qualifier=<VAR>    取得环境变量的值来做为输出信息的文件名。 [none]
  --log-socket=ipaddr:port  输出LOG到socket ，ipaddr:port

LOG信息输出
  --xml=yes                 将信息以xml格式输出，只有memcheck可用
  --num-callers=<number>        show <number> callers in stack traces [12]
  --error-limit=no|yes          如果太多错误，则停止显示新错误? [yes]
  --error-exitcode=<number>     如果发现错误则返回错误代码 [0=disable]
  --db-attach=no|yes            当出现错误，valgrind会自动启动调试器gdb。[no]
  --db-command=<command>    启动调试器的命令行选项[gdb -nw %f %p]

适用于Memcheck工具的相关选项：
  --leak-check=no|summary|full  要求对leak给出详细信息?  [summary]
  --leak-resolution=low|med|high    how much bt merging in leak check [low]
  --show-reachable=no|yes       show reachable blocks in leak check? [no]

 
## Valgrind 使用举例

```cpp
// 在编译时加上-g参数
gcc -g test.c -o test

// 运行 valgrind 中名为 tool 的工具，默认 memcheck，要求对 leak 给出详细信息
valgrind --tool=memcheck --leak-check=full ./test
```

下面是一段有问题的C程序代码test.c

```cpp
#include <stdlib.h>
void f(void)
{
   int* x = malloc(10 * sizeof(int));

   // 问题1: 数组下标越界 问题2: 内存没有释放
   x[10] = 0;     
}                 

int main(void)
{
   f();
   return 0;
}
```

1、    编译程序test.c
gcc -Wall test.c -g -o test
2、    使用Valgrind检查程序BUG
valgrind --tool=memcheck --leak-check=full ./test
3、    分析输出的调试信息
==3908== Memcheck, a memory error detector.
==3908== Copyright (C) 2002-2007, and GNU GPL'd, by Julian Seward et al.
==3908== Using LibVEX rev 1732, a library for dynamic binary translation.
==3908== Copyright (C) 2004-2007, and GNU GPL'd, by OpenWorks LLP.
==3908== Using valgrind-3.2.3, a dynamic binary instrumentation framework.
==3908== Copyright (C) 2000-2007, and GNU GPL'd, by Julian Seward et al.
==3908== For more details, rerun with: -v
==3908== 
--3908-- DWARF2 CFI reader: unhandled CFI instruction 0:50
--3908-- DWARF2 CFI reader: unhandled CFI instruction 0:50
/*数组越界错误*/
==3908== Invalid write of size 4                      
==3908==    at 0x8048384: f (test.c:6)
==3908==    by 0x80483AC: main (test.c:11)
==3908==  Address 0x400C050 is 0 bytes after a block of size 40 alloc'd
==3908==    at 0x40046F2: malloc (vg_replace_malloc.c:149)
==3908==    by 0x8048377: f (test.c:5)
==3908==    by 0x80483AC: main (test.c:11)
==3908== 
==3908== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 14 from 1)
==3908== malloc/free: in use at exit: 40 bytes in 1 blocks.   
==3908== malloc/free: 1 allocs, 0 frees, 40 bytes allocated.
==3908== For counts of detected errors, rerun with: -v
==3908== searching for pointers to 1 not-freed blocks.
==3908== checked 59,124 bytes.
==3908== 
==3908== 
/*有内存空间没有释放*/
==3908== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==3908==    at 0x40046F2: malloc (vg_replace_malloc.c:149)
==3908==    by 0x8048377: f (test.c:5)
==3908==    by 0x80483AC: main (test.c:11)
==3908== 
==3908== LEAK SUMMARY:
==3908==    definitely lost: 40 bytes in 1 blocks.
==3908==      possibly lost: 0 bytes in 0 blocks.
==3908==    still reachable: 0 bytes in 0 blocks.
==3908==         suppressed: 0 bytes in 0 blocks.

> Memcheck将内存泄露分为两种，一种是可能的内存泄露（Possibly lost），另外一种是确定的内存泄露（Definitely lost）。Possibly lost 是指仍然存在某个指针能够访问某块内存，但该指针指向的已经不是该内存首地址。Definitely lost 是指已经不能够访问这块内存。而Definitely lost又分为两种：直接的（direct）和间接的（indirect）。直接和间接的区别就是，直接是没有任何指针指向该内存，间接是指指向该内存的指针都位于内存泄露处。在上述的例子中，根节点是directly lost，而其他节点是indirectly lost。


## Reference

1. [Valgrind简介](http://www.turbolinux.com.cn/turbo/wiki/doku.php?do=show&id=valgrind)
2. [应用 Valgrind 发现 Linux 程序的内存问题](https://www.ibm.com/developerworks/cn/linux/l-cn-valgrind/)
