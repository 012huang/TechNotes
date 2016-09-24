
npm install -g gitbook-cli
gitbook -V

$ gitbook ls
There is no versions installed
You can install the latest version using: "gitbook fetch"

gitbook fetch

$ gitbook init
info: create chapter1/README.md
info: create chapter1/section1.1.md
info: create chapter1/section1.2.md
info: create chapter2/README.md
info: create SUMMARY.md
info: initialization is finished


$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 7 plugins are installed
info: loading plugin "livereload"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 5 pages
info: found 0 asset files
info: >> generation finished with success in 0.9s !

Starting server ...
Serving book on http://localhost:4000

## 使用

README.md 和 SUMMARY.md 是 Gitbook 项目必备的两个文件，也就是一本最简单的 gitbook 也必须含有这两个文件，它们在一本 Gitbook 中具有不同的用处。


## 插件

### ketax

### mathjax
npm i gitbook-plugin-mathjax
gitbook install


## Reference

https://github.com/GitbookIO/gitbook-cli
https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md
http://www.chengweiyang.cn/gitbook/
http://gitbook.zhangjikai.com/installation.html
[Gitbook Introduction - 陈斌彬的技术博客](https://cnbin.github.io/blog/2015/07/16/gitbook-introduction/)



gitbook toc number
https://github.com/GitbookIO/gitbook/issues/1323





