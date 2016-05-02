

## 介绍

[XPath](https://www.w3.org/TR/xpath/) 的全称是 XML Path Language，即 XML 路径语言，它是一种在结构化文档（比如 XML 和 HTML 文档）中定位信息的语言，关于 XPath 的介绍可以参考 https://www.w3.org/TR/xpath/。

## 语法

### HTML 实例文档

后面我们将以下面的 HTML 文档介绍 XPath 的使用。

```html
<html>
    <head>
        <base href='http://example.com/' />
        <title>Example website</title>
    </head>
    <body>
        <div id='images'>
            <a href='image1.html'>Name: My image 1 <br /><img src='image1_thumb.jpg' /></a>
            <a href='image2.html'>Name: My image 2 <br /><img src='image2_thumb.jpg' /></a>
            <a href='image3.html'>Name: My image 3 <br /><img src='image3_thumb.jpg' /></a>
            <a href='image4.html'>Name: My image 4 <br /><img src='image4_thumb.jpg' /></a>
            <a href='image5.html'>Name: My image 5 <br /><img src='image5_thumb.jpg' /></a>
        </div>
    </body>
</html>
```

### 选取节点

下表是 XPath 常用的语法，实例对应的是上面的 HTML 文档。

|  表达式  |              描述              |           实例           |                     结果                     |
|----------|--------------------------------|--------------------------|----------------------------------------------|
| nodename | 选取此节点的所有子节点         | body                     | 选取 body 元素的所有子节点                   |
| /        | 从根节点选取                   | /html                    | 选取根元素 html                              |
| //       | 匹配选择的当前节点，不考虑位置 | //img                    | 选取所有 img 元素，而不管它们在文档的位置    |
| .        | 选取当前节点                   | ./img                    | 选取当前节点下的 img 节点                    |
| ..       | 选取当前节点的父节点           | ../img                   | 选取当前节点的父节点下的 title               |
| @        | 选取属性                       | //a[@href="image1.html"] | 选取所有 href 属性为 "image1.html" 的 a 节点 |
|          |                                | //a/@href                | 获取所有 a 节点的 href 属性的值              |
|          |                                |                          |                                              |

### 谓语

> 谓语用来查找某个特定的节点或者包含某个指定的值的节点，谓语嵌在方括号中。

|        路径表达式        |                      结果                      |
|--------------------------|------------------------------------------------|
| //body/a[1]              | 选取属于 body 子元素的第一个 a 元素            |
| //body/a[last()]         | 选取属于 body 子元素的最好一个 a 元素          |
| //a[@href]               | 选取所有拥有名为 href 的属性的 a 元素          |
| //a[@href='image2.html'] | 选取所有 href 属性等于 "image2.html" 的 a 元素 |


## 在 Python 中使用

在 python 中使用 XPath 需要安装相应的库，这里推荐使用 [lxml]((http://lxml.de/)) 库。

代码示例：







[XML Path Language (XPath)](https://www.w3.org/TR/xpath/)
[lxml - Processing XML and HTML with Python](http://lxml.de/)
[XPath 语法](http://www.w3school.com.cn/xpath/xpath_syntax.asp)
[XPath、XQuery 以及 XSLT 函数](http://www.w3school.com.cn/xpath/xpath_functions.asp)
[xpath提取HTML // Astray Linux](http://astraylinux.com/2014/08/21/server-xpath-pick-html/)
[选择器(Selectors) — Scrapy 1.0.5 文档](http://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/selectors.html)





