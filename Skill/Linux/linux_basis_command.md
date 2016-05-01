


## 用户管理

- 创建用户和删除用户

```shell
# 创建用户命令：adduser 和 useradd
# adduser：自动为创建的用户指定主目录、系统 shell 版本，要求输入用户密码
# useradd：如果不添加任何参数，则创建出来的用户无主目录，无系统 shell 和无密码
$ sudo adduser test

# 删除用户命令：userdel
$ sudo userdel test
```


- 给用户添加 sudo 权限


```shell
1. 用root帐号登录或者su到root。

2. 增加sudoers文件的写权限： chmod u+w /etc/sudoers

3. vim /etc/sudoers 找到 root ALL=(ALL) ALL 在这行下边添加 dituhui ALL=(ALL) ALL  (ps:dituhui代表是你要添加sudo权限的用户名)

4. 除去sudoers文件的写权限： chmod u-w /etc/sudoers

http://blog.csdn.net/scottxu_5g/article/details/11778257
```

## 文件操作

### du

```
## 统计当前目录大小，去除某个文件夹
du -sh --exclude="YouCompleteMe" 

## 统计占用磁盘空间最大的前 10 个文件或文件夹，不包括隐藏文件
du -sh * | sort -rh | head -10

## 统计隐藏文件和文件夹大小
du -sh .*
```
