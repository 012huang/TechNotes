
<!-- MarkdownTOC -->

- [Develop](#develop)
- [命令行效率工具](#命令行效率工具)
- [System](#system)
- [Office](#office)
- [GTD](#gtd)
- [Network](#network)
- [Tips](#tips)
- [Reference](#reference)

<!-- /MarkdownTOC -->


## Develop
- Xcode & Xcode command line tools

```shell
$ xcode-select --install
```

- Sublime text3
    - [vkocubinsky/SublimeTableEditor](https://github.com/vkocubinsky/SublimeTableEditor)
- Eclipse
- iterm2 (brew, theme, zsh)
- Dash
    Dash is an API Documentation Browser and Code Snippet Manager. You can even generate your own docsets or request docsets to be included. http://kapeli.com/dash
- IntelliJ IDEA 15 CE
- PyCharm
- SourceTree
- macvim

```shell
两种安装方法
## 使用 brew
brew install macvim --with-override-system-vim

YouCompleteMe
./install.py --clang-completer (支持 C/C++)
./install.py --clang-completer --gocode-completer (确保已经安装 go)
./install.py --clang-completer  --tern-completer (确保已经安装 nodejs 和 npm)


## 直接下载二进制包，若想在 termianl 中使用
alias vim='mvim -v'
or alias vim="/Users/user/Applications/MacVim.app/Contents/MacOS/Vim"
```

- SnippetsLab
	
代码片段工具

- Python
    
不用系统自带的 python，用 brew 安装一个

```
brew install python --framework --universal
```

- [coda2](https://panic.com/coda/)
    
web 编程开发工具


## 命令行效率工具

- zsh
- ag, Like grep or ack, but faster.
- proxychains-ng
- polipo 为终端设置 socks 代理
- autojump
- tmux


## System
- Alfred
- Moom
- PopClip
- TextExpander
- CleanMyMac
- Entropy
	解压缩软件
- Bartender 2


## Office

- Xmind (MindNote, Novamind etc.)
- Evernote
- Leanote
- Baidu Pinyin
- Monodraw
	用来画 ASCII 流程图等

- Skim
- ShowHiddenFiles
- 百度云
- 坚果云


- Markdown
	- [Mweb](http://zh.mweb.im/)
	- Mou
	- Marked 2
	- Quiver
	- [farbox](https://www.farbox.com/service/app/desktop_editor)
	- [markeditor](http://markeditor.farbox.com/)

- PinPhoto
- Xee
- EasyMeasurer: 屏幕测量标尺工具，以像素为单位显示屏幕对象的距离




## GTD

- Doit.im
- Day one 2
- 滴答清单

## Network

- Chrome，常用扩展有:
    - [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega)
    - [evernote](https://chrome.google.com/webstore/detail/evernote-web-clipper/pioclpoplcdbaefihamjohnefbikjilc?hl=zh-CN)
    - [copy-as-markdown](https://github.com/chitsaou/copy-as-markdown), copy url as markdown
    - [octotree](https://github.com/buunguyen/octotree), Code tree for GitHub and GitLab
    - [vimium](https://github.com/philc/vimium)
    - [undirect](https://github.com/xwipeoutx/undirect), removes tracking and redirection from google search results
    - [Empty New Tab Page](https://chrome.google.com/webstore/detail/empty-new-tab-page/dpjamkmjmigaoobjbekmfgabipmfilij?hl=zh-CN)
    - [Firebug](https://chrome.google.com/webstore/detail/firebug-lite-for-google-c/bmagokdooijbeehmkpknfglimnifench)
    - [XPath Helper](https://chrome.google.com/webstore/detail/xpath-helper/hgimnogjllphhhkhlmebbmlgjoejdpjl)
    - [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc)
    - [1Password](https://1password.com/)
    - [react-devtools](https://github.com/facebook/react-devtools): An extension that allows inspection of React component hierarchy in Chrome Developer Tools
    - [speed-dial-2](https://chrome.google.com/webstore/detail/speed-dial-2/jpfpebmajhhopeonhlcgidhclcccjcik?hl=zh-CN) 快捷拨号插件，可自定义书签，快速访问
    - [infinity-new-tab](https://chrome.google.com/webstore/detail/infinity-new-tab/dbfmnekepjoapopniengjbcpnbljalfg?hl=zh-CN&gl=ID) 又一款快捷拨号插件，很精美


- GoAgentX
- Lantern
- Surge
- Astrill



## Tips

- QuickLook 增强

- Change the Notification Center banner dwell time in OS X
    defaults delete com.apple.notificationcenterui bannerTime
    defaults write com.apple.notificationcenterui bannerTime SECONDS
    defaults write com.apple.notificationcenterui bannerTime 2


- 光标闪烁频率（cursor blink rate）

```shell
defaults write -g NSTextInsertionPointBlinkPeriod -int 500
defaults write -g NSTextInsertionPointBlinkPeriod -int 1000000000
defaults write -g NSTextInsertionPointBlinkPeriodOn -float 999999999999 
defaults write -g CursorBlink -string 0
```

- 修改系统截图默认保存路径

```
defaults write com.apple.screencapture location ~/Pictures
killall SystemUIServer
```

- .DS_Store 配置

    DS_Store 用来存储文件显示属性的，比如文件图标的摆放位置等。
    
```
# 禁止.DS_store生成
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE

# 恢复.DS_store生成
defaults delete com.apple.desktopservices DSDontWriteNetworkStores

# 查找所有的 .DS_Store
find / -name ".DS_Store"
```





## Reference

1. [Change the Notification Center banner dwell time in OS X](http://www.cnet.com/news/change-the-notification-center-banner-dwell-time-in-os-x/)
2. [Change How Long Notification Banners Persist for in OS X](http://osxdaily.com/2014/01/29/change-notifications-banner-time-mac-os-x/)







