
<!-- MarkdownTOC -->

- [Develop](#develop)
- [System](#system)
- [Office](#office)
- [GTD](#gtd)
- [Network](#network)
- [Tips](#tips)
- [Reference](#reference)

<!-- /MarkdownTOC -->


## Develop
- Xcode
- Sublime text3
- Eclipse
- iterm2 (brew, theme, zsh)
- Dash
- IntelliJ IDEA 15 CE
- PyCharm
- SourceTree

- macvim


```shell
两种安装方法
## 使用 brew
brew install macvim --with-override-system-vim

YouCompleteMe
./install.py --clang-completer --gocode-completer


## 直接下载二进制包，若想在 termianl 中使用
alias vim='mvim -v'
alias vim="/Users/user/Applications/MacVim.app/Contents/MacOS/Vim"
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




## GTD

- Doit.im
- Day one 2


## Network

- Chrome (SwitchOmega, evernote)
- GoAgentX
- Lantern
- Surge
- Astrill



## Tips

- QuickLook 增强


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





## Reference

1. [Change the Notification Center banner dwell time in OS X](http://www.cnet.com/news/change-the-notification-center-banner-dwell-time-in-os-x/)
2. [Change How Long Notification Banners Persist for in OS X](http://osxdaily.com/2014/01/29/change-notifications-banner-time-mac-os-x/)







