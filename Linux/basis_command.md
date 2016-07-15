


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


## 数学运算

### 进制转换

```shell
## obase 是输出进制，ibase 是输入进制
echo 'obase=10;ibase=16;4E25' | bc
```

tips: 当您设置 bc 的输入进制以后，输入 bc 的所有数字都使用该进制，包括您提供用于设置输出进制的数字。因此最好先设置输出进制，否则可能会产生意想不到的结果



## link

命令格式：
 ln [参数][源文件或目录][目标文件或目录]

 - `ln` 命令会保持每一处链接文件的同步性，也就是说，不论你改动了哪一处，其它的文件都会发生相同的变化；
 - `ln` 的链接又分『软链接』和『硬链接』两种，软链接就是 `ln –s 源文件 目标文件`，它只会在你选定的位置上生成一个文件的镜像，
    不会占用磁盘空间，硬链接 `ln 源文件 目标文件`，它会在你选定的位置上生成一个和源文件大小相同的文件， 
 - 无论是软链接还是硬链接，文件都保持同步变化。


