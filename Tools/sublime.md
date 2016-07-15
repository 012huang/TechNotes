

## 插件

- HTML-CSS-JS Prettify: 格式化 HTML 代码



- 大小写转换

ctrl+K+ctrl+U ====转换文字为大写

ctrl+K+ctrl+I   ====转换文字为小写

将单词的首字母转换为大写没有快捷键你可以从指令面板呼叫 ==title case,或者是自己设定快捷键例如加上这一行就可以利用ctrl+K+ctrl+T 呼叫他：

json [ { "keys": ["super+k", "super+t"], "command": "title_case" } ]


- 尺规

尺规会显示一条参考线，用来限制单行显示的字元数量。有人认为这样有助于程序码的阅读你可以从view>>ruler去选择要断行的字数，这样编辑器上就会显示一条参考线也可以从偏好设定中加上自定的数值，或是显示多条参考线 例如

[

       " rulers": [90,110,130]

]
