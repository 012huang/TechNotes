---
title: "Alfred 杀手级插件: Google Search"
date: 2016/06/22 11:19
tags: [alfred, tools]
categories: 工具
---


# 简介

> 和大家分享我自己打造的一个谷歌搜索插件: [Google-Alfred-Workflow](https://github.com/ethan-funny/Google-Alfred3-Workflow)

我平时写代码，写博客的时候经常免不了要谷歌一下，这时我一般唤醒 Alfred，然后输入搜索关键词，跳转到 Chrome 浏览器，查看搜索结果。另外，我在写博客的时候，经常需要获取某个网站的链接，比如想获取 Django 或者 Flask 或者 Bottle 的官网链接，这时我也是唤醒 Alfred，输入 Django，跳转到 Chrome 浏览器，复制想要的官网链接。这对于程序猿而言，简直不能忍受。于是，我就开始打造自己的一个谷歌搜索插件。

# 功能

目前插件看起来是这样子的：

![google-search-result-2](http://7xiht5.com1.z0.glb.clouddn.com/google-search-2.png-ab)

插件支持的功能主要有：

- 输入 `gs`，以及关键词，实时查询搜索结果（标题+链接）

- `Enter` 键直接跳转到链接所在页面

- `Command + Enter` 键直接复制链接

![copy-link](http://7xiht5.com1.z0.glb.clouddn.com/copy-link.png)

- `Option + Enter` 键复制 markdown 形式的链接

![copy-link-with-markdown-format](http://7xiht5.com1.z0.glb.clouddn.com/copy-link-with-markdown-format.png)

## 配置

由于我们不能直接访问谷歌，所以插件也提供了 `socks5` 代理的设置，以便可以访问谷歌，这就需要你本机已经配置好了 `socks` 代理，这应该也是必备的吧。比如我用的是 [shadowsocks](https://shadowsocks.com/)，本机电脑使用的是 `GoAgentX`，`GoAgentX` 的配置类似如下：

![goagentx](http://7xiht5.com1.z0.glb.clouddn.com/goagentx.png-ab)

Alfred 插件的配置只需要配置本地的代理端口，比如 GoAgentX 中的本地端口是 1234，那么 Alfred 插件的代理端口也要配置 1234，如下：

![configure proxy port](http://7xiht5.com1.z0.glb.clouddn.com/config-proxy-port.png)

如果你不想用 socks 代理的话（默认是不启用的），你可以输入 `gsc 0`。


# 最后

如果大家在使用过程中有什么问题的话，欢迎提出来。希望该插件可以提升你的工作效率，我改天也写一篇是怎么制作改插件的。

[插件下载](https://github.com/ethan-funny/Google-Alfred3-Workflow)。

