---
title: "Python 中 datetime 和 second 之间的转换"
date: 2016/08/08 16:05
tags: [python]
categories:  Python

---

## 计算两个 datetime 之间的秒数

```python
import datetime

a = datetime.datetime(2013,12,30,23,59,59)
b = datetime.datetime(2013,12,31,23,59,59)

print (b-a).total_seconds()
86400.0
```

## 将秒数转为 day hour:minute:second

```python
>>> import datetime
>>> print str(datetime.timedelta(seconds=3661))
1:01:01
>>> print str(datetime.timedelta(seconds=86401))
1 day, 0:00:01
```

## 参考资料

- [python - How do I check the difference, in seconds, between two dates? - Stack Overflow](http://stackoverflow.com/questions/4362491/how-do-i-check-the-difference-in-seconds-between-two-dates)
- [Python Time Seconds to h:m:s - Stack Overflow](http://stackoverflow.com/questions/775049/python-time-seconds-to-hms)


