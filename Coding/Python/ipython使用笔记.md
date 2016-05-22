

进入终端，使用命令 `ipython` 进去 ipython 的交互环境。


## 在 ipython 中执行脚本

$ ipython
> run ipython_context.py
> dir() # 查看变量

## 帮助

?command
??command

## 保存会话

%save: 保存输入命令到文件。
可以将多个范围的输入数据保存到文件中。通常用于将交互环境中写的测试代码保存成源码文件。

%save -r test.txt 33-34 36
保存33-34(闭区间)以及36行到当前目录下test.txt文件里
参数 -a 添加到结尾

%history -f path/to/file


%logstart: 启动记录器。
%logon: 开始记录。
%logoff: 暂停记录。
%logstate: 查看记录状态。
%logstop: 关闭记录器。


%logstart -t 加上时间戳
会自动创建一个名为 `ipython_log.py` 的文件

This will create a uniquely named .py file and store your session for later use as an interactive Ipython session or for use in the script(s) of your choosing.


[shell - How to save a Python interactive session? - Stack Overflow](http://stackoverflow.com/questions/947810/how-to-save-a-python-interactive-session)

[ipython使用笔记](http://blog.just4fun.site/learning-ipython.html)


[IPython 用法 — z42-doc 0.1 文档](http://z42.readthedocs.io/zh/latest/devtools/ipython.html)




