

## 匹配中文

假设现在想把字符串 `title = u'你好，hello，世界'` 中的中文提取出来，

由于[中文的 unicode 编码范围](http://blog.oasisfeng.com/2006/10/19/full-cjk-unicode-range/)是 `[\u4e00-\u9fa5]`，因此可以这么做：


```python
import re
title = u'你好，hello，世界'
pattern = re.compile(ur'[\u4e00-\u9fa5]+')
result = re.findall(pattern, title)
for item in result:
    print item
```

```shell
# 输出
你好
世界
```


