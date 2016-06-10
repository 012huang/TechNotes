


# vim使用

## 安装

### mac平台

```
brew update 
brew install vim 
brew install macvim –override-system-vim
brew linkapps macvim
vi .bash_profile 
alias vim=”/Applications/MacVim.app/Contents/MacOS/Vim” 
source .bash_profile
```

## 移动or跳转
```
1. vi移动到屏幕下一行: gj
2. 上下左右: jkhl
3. vim的jumplist，往前跳和往后跳的快捷键为Ctrl+O以及Ctrl+I
```

## 查找
1. 精确匹配查找单词如果你输入 "/the"，你也可能找到 "there".
* 要找到以 "the"结尾的单词，可以用：```/the\>```，"```\>```"是一个特殊的记号，表示只匹配单词末尾。
* 类似地，"```\<```" 只匹配单词的开头。
* 这样，要匹配一个完整的单词 "the"，只需:```/\<the\> ```

## 替换
1. 将全文的tab键改为四个空格，命令是
```
:%s/ctr+I/    /g (空白处是四个空格)
```


## 窗口分屏

```
上下分割，并打开一个新的文件
:sp filename

左右分割，并打开一个新的文件
:vsp filename

新建窗口:（crtl + w） n
分割窗口: (ctrl + w) s
垂直分割窗口: (ctrl + w) v
关闭当前窗口: (ctrl + w) c
关闭其它窗口: (ctrl + w) o
向上轮换窗口: (ctrl + w) R
向下轮换窗口: (crtl + w) r
使窗口等宽: (crtl + w) =
使窗口最小化: (ctrl + w) 1_
使窗口最大化:  (crtl + w) _
使窗口向左最小化: (crtl +w ) 1|
使窗口向右最大化: (crtl + w) |
将缓冲区分割到一个窗口中: (crtl + w) ^
两个窗内容切换: (crtl + w) x
两个窗横屏变竖屏: (crtl + w) H
两个窗竖屏变横屏: (crtl + w) K

将当前窗口增加/减少n行: (ctrl + w) n +/-
将当前窗口增加/减少n列: (ctrl + w) n >/<
```

## 宏使用（recording）

### 具体使用

```
第一步：在正常模式下（非insert模式、非visual模式）按下q键盘

第二步：选择a-z或0-9中任意一个作为缓冲器的名字，准备开始录制宏

第三步：正常的操作，此次所有的操作都会被记录在上一步中定义的缓冲器中

第四步：在非insert模式下输入q停止宏的录制

第五步：使用@ + 第二步中定义的缓冲器的名字即可。
```

例如想把文字

```
line1
line-2
line3-1
l4
```

变成如下的文字

```
System.out.println(line1);
System.out.println(line1);
System.out.println(line-2);
System.out.println(line3-1);
System.out.println(L4);
```

步骤如下：

- 首先把光标移动line1上，输入qt，准备开始录制，缓冲器的名字为t，
- 录制的动作为：0 回到行首、按下 i 键进入 insert 模式、输入“System.out.println(”、按下esc键回到正常模式、shift + $ 回到行尾部、按下i键进入insert模式、输入“);”
- 按下esc键回到正常模式，按下q停止录制。然后把光标移动到下面一行的任意位置输入 @ + t 即可。

recording还可以和查询结合起来使用，例如想把一个文件中含有特定字符串的行注释，可以通过这样的宏来实现。在正常模式下输入/search string + enter、shift + ^、i、#、esc、shift + $。

让定制的宏自动执行多次的方法是先输入一个数字，然后在输入@ + 缓冲器的名字。 例如 100@t，表示执行100次


### 修改宏

当你发现存在某个寄存器的命令宏是错误的，你除了可以重新写一遍命令宏之外，还有如下修改方式：
1、先用G（大写）到文件末尾，然后用o（小写）新加一行，不要编辑，用ESC退出到普通模式，其实就是为编辑宏找了个地方。(或用 new 开一个新窗口)
2、使用命令 ```"tp```会看到寄存器 t 中的命令宏像文本一样出现在这一行，然后编辑这一行。编辑的时候与vim编辑其他的文件一样。编辑结束后用0（零）回到行首。
3、然后用 ```"ty$``` 将正确内容写到寄存器a中，最后删除这一行即可。
4、当你需要向命令宏寄存器中增加内容时，可以用命令 ```qA``` 来向 ```t``` 寄存器增加内容，之后输入你想增加的内容，再使用q结束。

## 插件
### [EasyMotion](https://github.com/easymotion/vim-easymotion)

```
vimrc配置
" 更改快捷键
map f <Plug>(easymotion-prefix)
map ff <Plug>(easymotion-s)
map fs <Plug>(easymotion-f)
map fl <Plug>(easymotion-lineforward)
map fj <Plug>(easymotion-j)
map fk <Plug>(easymotion-k)
map fh <Plug>(easymotion-linebackward)
" 忽略大小写
let g:EasyMotion_smartcase = 1

常用快捷键：
ff 全屏搜索
fs 往下搜索
fF 往上搜索
fl 行内向右搜索
fj 行间向下搜索
fk 行间向上搜索
fh 行内向左搜索
fw 往下搜索一个单词开始处
fb 往上搜索一个单词开始处
fe 往下搜索一个单词结尾处
fge 往下搜索一个单词结尾处
```

### [NERD Commenter](https://github.com/scrooloose/nerdcommenter)

```
常用快捷键
<leader>cc 注释当前行
<leader>cm 只用一组符号来注释
<leader>cy 注释并复制
<leader>cs 优美的注释
<leader>cu 取消注释
<leader>ci 原先注释的地方反注释，未注释的地方注释
<leader>c$ 从当前字符注释到行尾。
<leader>cA 在行尾添加注释
<leader>cl 左对齐注释，两端对齐的注释
```

### tagbar

```
<CR>/<Enter>  跳转到当前光标下的 tag。如果是伪标签或一般的头信息则没作用.
p             源文件跳转到当前光标下的 tag。但光标停留在 Tagbar 窗口。
<Space>       在命令行显示当前 tag 的原型信息。(比如行号)
+/zo          打开当前光标下的折叠。
-/zc          如果光标下有折叠则关闭光标下的折叠，如果没有则关闭当前的折叠。
o/za          切换光标下的折叠状态，如果光标下没有折叠，切换当前的折叠状态。
*/zR          通过设置折叠级别(foldlevel)为 99 来打开所有的折叠。
=/zM          通过设置折叠级别为 0 来关闭所有的折叠。
<C-N>         转到下一个顶层 tag。
<C-P>         转到前一个顶层 tag。
s             在 tag 名称排序和文件顺序排序中切换。
x             切换 Tagbar 窗口的最大化。
q             关闭 Tagbar 窗口。
```

### vim-surround
#### deleting surroundings (ds)
Surroundings can be deleted with the **"ds"** command. After you type "ds", the command expects the surrounding target you want to delete. It may be any of three quote marks, ', ", and `, the eight punctuation marks, (, ), {, }, [, ], <, > , and a special 't' target for deleting the innermost HTML tag.
```
Text              Command    New Text
---------------   -------    -----------
'Hello W|orld'    ds'        Hello World
(12|3+4*56)/2     ds(        123+4*56/2
<div>fo|o</div>   dst        foo

(| is the position of cursor in these examples)
```
#### Examples of deleting surroundings (cs)
Surroundings can be changed with the "cs" command. The "cs" command, just like "ds" command takes a surrounding target, and it also takes the surrounding replacement. There are a few more surrounding targets for this command. They are w for word, W for word + skip punctuation, s for sentence, and p for paragraph.

```
Text              Command    New Text
---------------   -------    -----------
"Hello |world!"   cs"'       'Hello world!'
"Hello |world!"   cs"<q>     <q>Hello world!</q>
(123+4|56)/2      cs)]       [123+456]/2
(123+4|56)/2      cs)[       [ 123+456 ]/2
<div>foo|</div>   cst<p>     <p>foo</p>
fo|o!             csw'       'foo'!
fo|o!             csW'       'foo!'

(| is the position of cursor in these examples)
```

#### adding surroundings(ys)
Surroundings can be added with the same "cs" command, which takes a surrounding target, or with the "ys" command that takes a valid vim motion. There is a special "yss" command that applies a surrounding to the whole line, and "ySS" that applies the surrounding to the whole line, places the text on a new line and indents it.
```
Text              Command      New Text
---------------   -------      -----------
Hello w|orld!     ysiw)        Hello (world)!
Hello w|orld!     csw)         Hello (world)!
fo|o              ysiwt<html>  <html>foo</html>
foo quu|x baz     yss"         "foo quux baz"
foo quu|x baz     ySS"         "
                                   foo quux baz
                               "

(| is the position of cursor in these examples)
```
#### short cut
```
Normal mode
-----------
ds  - delete a surrounding
cs  - change a surrounding
ys  - add a surrounding
yS  - add a surrounding and place the surrounded text on a new line + indent it
yss - add a surrounding to the whole line
ySs - add a surrounding to the whole line, place it on a new line + indent it
ySS - same as ySs

Visual mode
-----------
s   - in visual mode, add a surrounding
S   - in visual mode, add a surrounding but place text on new line + indent it
```

### vim-airline
#### 配置powerline

```
~ $ git clone https://github.com/powerline/fonts.git
~ $ cd fonts
~ $ ./install.sh

安装完成后我们就可以在iTerm2或者Terminal的字体选项里看到并选择多个xxx for powerline的字体了。*注意：对于ASCII fonts和non-ASCII fonts都需要选择for powerline的字体

airline配置
let g:airline_powerline_fonts = 1
```


## 命令
在vi内使用linux命令，使用! 
```
如在tr命令前要加上您希望处理的行范围和感叹号 （！），如 
1,$!tr -d '\t'(美元符号表示最后一行)
```
## QuickFix
```
:make " 編譯程式

:copen " 打開QF視窗
:cclose " 關閉QF視窗

:cnext " 移到下一個錯誤
:cprev " 移到前一個錯誤

:cnewer " 若有多個QF buffer，移到下一個錯誤訊息列表
:colde " 若有多個QF buffer，移到前一個錯誤訊息列表
```

## tips

```
ctrl + v + i - 输入tab键
gf – 打开光标处所指的文件（这个命令在打到#include头文件时挺好用的，当然，仅限于有路径的）
Ctrl + O - 向后回退你的光标移动
Ctrl + I - 向前追赶你的光标移动
```
### 打开文件
在mac下，打开find出来的文件
```
find . -name case.sh | xargs -o vim 或者 vi find . -name "case.sh"
```

## Reference
1 [vim小技巧](http://www.cnitblog.com/hustwei/archive/2008/05/21/44034.html)
2. [无插件vim编程技巧](http://coolshell.cn/articles/11312.html)
3. [Vim快捷键键位图](http://cenalulu.github.io/linux/all-vim-cheatsheat/)
4. [spf13-vim](https://github.com/spf13/spf13-vim)
5. [tagbar 使用](https://github.com/vimcn/tagbar.cnx)
6. [vim recording功能介绍](http://www.netingcn.com/vim-recording-function.html)
7. [vim 宏的录制和使用](http://blog.csdn.net/yangzhongxuan/article/details/7001077)
