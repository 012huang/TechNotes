
```
from lxml import etree

page_etree = etree.HTML(page_source)
type(page_etree) -> lxml.etree._Element
```

> from lxml.etree import tostring
> tostring(page_etree)


lxml.etree._Element
    - getprevious()
    - getchildren()
    - getnext()
    - getparent()
    - xpath()
    - cssselect()

    - tag
    - keys()
    - values()
    - attrib
    - text


注意:
lxml 3.5.0 以上 lxml.etree._Element 才有 cssselect() 等这些方法，如果是 3.5.0 以下的，可以使用

```
from lxml.html import fromstring
page_etree = fromstring(page_source)
```

## Reference

- [Bug #1490451 “Please support cssselect() in lxml.etree, not just...”](https://bugs.launchpad.net/lxml/+bug/1490451)

- [python - lxml: cssselect(): AttributeError: 'lxml.etree._Element' object has no attribute 'cssselect' - Stack Overflow](http://stackoverflow.com/questions/32264533/lxml-cssselect-attributeerror-lxml-etree-element-object-has-no-attribute)


