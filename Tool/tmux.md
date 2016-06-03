

# Tmux Usage

## ShortCut

- ```prefix + space```
    - Convert 2 horizontal panes to vertical panes in tmux.
    - (bound to next-layout by default) cycles through available layouts, you can also use the select-layout command.

- ```prefix + $```
    - rename session name

- ```prefix + ,```
    - rename window name

- ``` prefix + s ```
    - select session

- ``` prefix + c```
    - new window


## command

### new session

```
tmux new-session -s "session_name"
```

### rename session
```
shortcut: prefix + $
```

### new window
```
tmux new-window -n "window name"
shortcut: prefix + c
```

### attach session
```
tmux attach -t "session name"
tmux attach
```
### select session
```
shortcut: prefix + s
```

### session list
```
tmux ls
```

### kill session
```
tmux kill-session -t "seesion name"
```


## Reference
- [tmux: Productive Mouse-Free Development](https://github.com/aqua7regia/tmux-Productive-Mouse-Free-Development_zh)
- [how-to-convert-2-horizontal-panes-to-vertical-panes-in-tmux](http://superuser.com/questions/493048/how-to-convert-2-horizontal-panes-to-vertical-panes-in-tmux)

