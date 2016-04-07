<!-- MarkdownTOC -->

- [boost](#boost)
	- [安装](#安装)
	- [使用](#使用)
		- [命令行](#命令行)
	- [Reference](#reference)

<!-- /MarkdownTOC -->

# boost

## 安装

```shell
## 安装
brew install boost

## 安装目录在/usr/local/Cellar/boost
## 头文件：/usr/local/include
## 库文件：/usr/local/lib
```

## 使用

### 命令行

```shell

## 将下面内容加到 ~/.bashrc or ~/.zshrc
## 根据实际路径修改

BOOST_INCLUDE=/usr/local/include
export BOOST_INCLUDE

BOOST_LIB=/usr/local/lib
export BOOST_LIB

$ g++ -o samlpe.out samlpe.cpp -I$BOOST_INCLUDE -L$BOOST_LIB -lboost_thread-mt -lboost_system -lboost_system-mt

## 或直接输入路径
$ g++ test.cpp -I /usr/local/include -L /usr/local/lib -lboost_thread-mt -lboost_system -lboost_system-mt -o test
```

写一个如下所示的cpp文件。

```cpp
//samlpe.cpp
#include <iostream>
#include <string>
#include <boost/thread.hpp>

using namespace std;

void threadRoutine(void)
{
    boost::xtime time;
    time.nsec = 0;
    time.sec = 20;
    cout << "线程函数做一些事情" << endl;
    boost::thread::sleep(time);    
}

int main(void)
{
    string str;
    cout << "输入任意字符开始创建一个线程..." << endl;
    cin >> str;
    boost::thread t(&threadRoutine);
    t.join();
    cout << "输入任意字符结束运行..." << endl;
    cin >> str;
    return 0;
}

保存。使用g++编译，命令如下所示：

g++ -o samlpe.out samlpe.cpp -I$BOOST_INCLUDE -L$BOOST_LIB -lboost_thread-mt -lboost_system -lboost_system-mt

g++ test.cpp -I /usr/local/include -L /usr/local/lib -lboost_thread-mt -lboost_system -lboost_system-mt -o test

其中-I参数指定Boost头文件路径，-L参数指定Boost库文件路径，-l参数指定使用线程库名。在我使用的这个版本Boost里，到/usr/local/lib/boost路径下，可以看到有关Boost线程库文件，比如：libboost_thread-mt.a等。注意在用-l 参数指定库名时把磁盘文件名前面那个lib前缀去掉就可以了。
```

## Reference
[Linux下G++怎么编译使用Boost库的程序](http://szvcn.blog.163.com/blog/static/1867963200922873535471/)


