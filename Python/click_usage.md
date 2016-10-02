---
title: "Python 中使用 Click 解析命令行参数"
date: 2016/07/22 17:12
tags: [python]
categories: Python

---

```python
import click

@click.command()
@click.option('--count', default=1, help='Number of greetings.')
@click.option('--name', prompt='Your name',
              help='The person to greet.')
def hello(count, name):
    """Simple program that greets NAME for a total of COUNT times."""
    for x in range(count):
        click.echo('Hello %s!' % name)

if __name__ == '__main__':
    hello()
```

```
$ python hello.py --count=2
Your name: xiaoh
Hello xiaoh!
Hello xiaoh!

$ python hello.py --help
Usage: hello.py [OPTIONS]

  Simple program that greets NAME for a total of COUNT times.

Options:
  --count INTEGER  Number of greetings.
  --name TEXT      The person to greet.
  --help           Show this message and exit.
```





# 参考资料

- [Click](http://click.pocoo.org/6/)
- [Python Click Command 快速入门](http://www.xiaoh.me/2016/01/29/click-command/)



