# argparse

## 定位参数

```py
$ cat prog.py
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("square", help="display a square of a given number", type=int)
args = parser.parse_args()
print args.square**2

$ python prog.py 9
81
```

## 可选参数

```py
$ cat prog.py
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--square", help="display a square of a given number",
                    type=int)

parser.add_argument("--cubic", help="display a cubic of a given number",
                            type=int)

args = parser.parse_args()

if args.square:
    print args.square**2

if args.cubic:
    print args.cubic**3

$ python prog.py --help
usage: prog.py [-h] [--square SQUARE] [--cubic CUBIC]

optional arguments:
  -h, --help       show this help message and exit
  --square SQUARE  display a square of a given number
  --cubic CUBIC    display a cubic of a given number
$
$ python prog.py --square 9
81
$
$ python prog.py --cubic 9
729
```

## 混合使用

```
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("square", type=int,
                    help="display a square of a given number")
parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2],
                    help="increase output verbosity")
args = parser.parse_args()
answer = args.square**2
if args.verbosity == 2:
    print "the square of {} equals {}".format(args.square, answer)
elif args.verbosity == 1:
    print "{}^2 == {}".format(args.square, answer)
else:
    print answer
```

```
$ python prog.py 4 -v 3
usage: prog.py [-h] [-v {0,1,2}] square
prog.py: error: argument -v/--verbosity: invalid choice: 3 (choose from 0, 1, 2)
$ python prog.py 4 -h
usage: prog.py [-h] [-v {0,1,2}] square

positional arguments:
  square                display a square of a given number

optional arguments:
  -h, --help            show this help message and exit
  -v {0,1,2}, --verbosity {0,1,2}
                        increase output verbosity
```

```
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("x", type=int, help="the base")
parser.add_argument("y", type=int, help="the exponent")
parser.add_argument("-v", "--verbosity", action="count", default=0)
args = parser.parse_args()
answer = args.x**args.y
if args.verbosity >= 2:
    print "Running '{}'".format(__file__)
if args.verbosity >= 1:
    print "{}^{} ==".format(args.x, args.y),
print answer

$ python prog.py 4 2
16
$ python prog.py 4 2 -v
4^2 == 16
$ python prog.py 4 2 -vv
Running 'prog.py'
4^2 == 16

```


### 增加参数

```
ArgumentParser.add_argument(name or flags...[, action][, nargs][, const][, default][, type][, choices][, required][, help][, metavar][, dest])
```


每个参数解释如下:
name or flags - 参数的名字.
action - 遇到参数时的动作，默认值是store。store_const，表示赋值为const；append，将遇到的值存储成列表，也就是如果参数重复则会保存多个值; append_const，将参数规范中定义的一个值保存到一个列表；count，存储遇到的次数；此外，也可以继承argparse.Action自定义参数解析；
nargs - 参数的个数，可以是具体的数字，或者是?号，当不指定值时对于Positional argument使用default，对于Optional argument使用const；或者是*号，表示0或多个参数；或者是+号表示1或多个参数.
const - action和nargs所需要的常量值.
default - 不指定参数时的默认值.
type - 参数的类型.
choices - 参数允许的值.
required - 可选参数是否可以省略(仅针对optionals).
help - 参数的帮助信息，当指定为`argparse.SUPPRESS`时表示不显示该参数的帮助信息.
metavar - 在usage说明中的参数名称，对于必选参数默认就是参数名称，对于可选参数默认是全大写的参数名称.
dest - 解析后的参数名称，默认情况下，对于可选参数选取最长的名称，中划线转换为下划线.

```
# 参数名称为echo
parser.add_argument("echo", help="echo the string you use here")
# 可以增加类型
parser.add_argument("square", help="display a square of a given number",
                type=int)
# 可选参数前面多了--符号，-v是简写形式，store_true说明碰到该参数时保存为true，否则就是false
parser.add_argument("-v", "--verbose", help="increase output verbosity",
                action="store_true")
# 当然，也可以这样写，规定了可选参数的类型和取值范围
parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2],
                help="increase output verbosity")
# count表示遇到该参数几次，值就加几，默认值是0
parser.add_argument("-v", "--verbosity", action="count", default=0,
                help="increase output verbosity")
```


## 参考链接

- [Argparse Tutorial — Python 2.7.12 documentation](https://docs.python.org/2/howto/argparse.html)


