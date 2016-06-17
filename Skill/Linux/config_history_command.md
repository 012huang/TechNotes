
# history command

## bash

```
往 /etc/bashrc 添加export HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S  "
source /etc/bashrc
再source .bashrc
```

## zsh
zsh 不太一样：

```
which history
history: aliased to fc -l 1
vi .zhsrc
HIST_STAMPS="yyyy-mm-dd [H:M:S] "
source .zshrc
```

```
history | head -10
    1  2015-04-28 15:47  ll
    2  2015-04-28 15:48  vi .zprofile
    3  2015-04-28 15:49  source .zprofile
    4  2015-04-28 15:49  ll
    5  2015-04-28 15:50  source .bash_profile
    6  2015-04-28 15:50  source .zprofile
    7  2015-04-28 15:54  zsh --versin
    8  2015-04-28 15:54  zsh --version
    9  2015-04-28 15:54  wget
   10  2015-04-28 15:54  curl

history | tail -10
 6854  2015-07-18 23:37  fc -il 10 1
 6855  2015-07-18 23:37  fc -il 1 10
 6856  2015-07-18 23:41  history
 6857  2015-07-18 23:41  history | less
 6858  2015-07-18 23:42  history | less 10
 6859  2015-07-18 23:42  history | less -10
 6860  2015-07-18 23:42  history | head -10
 6861  2015-07-18 23:42  history | tail -10
 6862  2015-07-18 23:43  vi .zsh_history
 6863  2015-07-18 23:43  history
```

或直接使用

```
fc -il
 6913  2015-07-19 10:21  ttyplay ttyrecord
 6914  2015-07-19 10:22  cls
 6915  2015-07-19 10:22  ll
 6916  2015-07-19 10:22  ttyplay ttyrecord
 6917  2015-07-19 10:22  ttyplay myrecoding
 6918  2015-07-19 10:25  cls
 6919  2015-07-19 10:25  ll
 6920  2015-07-19 10:25  vi test
 6921  2015-07-19 10:25  vi myrecoding
 6922  2015-07-19 10:25  rm myrecoding ttyrecord typescript
 6923  2015-07-19 10:25  cls
 6924  2015-07-19 10:25  ll
 6925  2015-07-19 10:26  fc -l
 6926  2015-07-19 10:26  fc -lE
 6927  2015-07-19 10:26  history -E
 6928  2015-07-19 10:26  history E
```


