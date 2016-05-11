

# mysql


## 安装

```
## 安装最新版
brew install mysql

## 安装某个版本
brew install homebrew/versions/mysql55
```

## 启动

### 开机自动启动

```shell
ln -sfv /usr/local/opt/mysql55/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql55.plist

# 或者
/usr/local/opt/mysql55/bin/mysql.server start
/usr/local/Cellar/mysql55/5.5.44/support-files/mysql.server start
```


### 查看是否启用

mysql的默认端口号是3306，通常mysql的服务名都是mysqld。

```shell
## 查看所有端口号及其对应的服务
$ vi /etc/services 

$ ps -ef | grep mysql
$ netstat -an | grep 3306
$ lsof -i:3306
```

### 关闭

```
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mysql55.plist

# or
/usr/local/opt/mysql55/bin/mysql.server start
/usr/local/Cellar/mysql55/5.5.44/support-files/mysql.server stop
```

## 连接

- MySQL连接本地数据库，用户名为“root”，密码“123”（注意：“-p”和“123” 之间不能有空格）

```
$ mysql -h localhost -u root -p123（注意-p与密码是紧跟的）
```

- MySQL连接远程数据库（192.168.0.201），端口“3306”，用户名为“root”，密码“123”

```
$ mysql -h 172.16.16.45 -P 3306 -u root -p123
```

- MySQL连接本地数据库，用户名为“root”，隐藏密码

```
$ mysql -h localhost -u root -pEnter password:
```

- MySQL 连接本地数据库，用户名为“root”，指定所连接的数据库为“test”

```
$ mysql -h localhost -u root -p123 -D test
```

## 使用

```shell
## 初始没有设置密码
$ mysql -u root password 123456
mysql > create database <数据库名> ## 创建数据库
mysql > show databases; ## 显示所有的数据库
mysql > drop database <数据库名>; ## 删除数据库
mysql > use <数据库名>; ## 连接数据库
mysql > select database(); ## 查看当前使用的数据库
mysql > show tables; ## 查看当前数据库包含的表信息
mysql > show tables from <数据库名> ## 查看某个数据库包含的表信息
mysql > select * from <表名> ## 查询所有数据
mysql > show variables;
mysql > show global variables like 'port';
mysql > quit;
```

### 备份数据库

``` shell
1. source 命令
## 进入 mysql 数据库控制台
$ mysql -u root
mysql> use <数据库名>;
## source 脚本文件
mysql> source file.sql

2. 备份命令 mysqldump 
$ mysqldump -h主机名 -P端口 -u用户名 -p密码 -database 数据库名 > file.sql
$ mysqldump -uroot -p123456 --database itemdata > itemdata.sql

3. mysql 命令
mysql -u username -p -D dbname > file.sql
```

### select 语句

- 选择 id 列等于某个值的记录

```
select * from user where id='53421cea63051f5c0371eaf9';
```

### 基本语句

```
(1) 数据记录筛选：
sql="select * from 数据表 where 字段名=字段值 order by字段名[desc]"（按某个字段值降序排列。默认升序ASC）
sql="select * from 数据表 where字段名like '%字段值%' order by 字段名 [desc]"
sql="select top 10 * from 数据表 where字段名=字段值 order by 字段名 [desc]"
sql="select top 10 * from 数据表 order by 字段名 [desc]"
sql="select * from 数据表 where字段名in ('值1','值2','值3')"
sql="select * from 数据表 where字段名between 值1 and 值2"
(2) 更新数据记录：
sql="update 数据表 set字段名=字段值 where 条件表达式"
sql="update 数据表 set 字段1=值1,字段2=值2 …… 字段n=值n where 条件表达式"
(3) 删除数据记录：
sql="delete from 数据表 where 条件表达式"
sql="delete from 数据表" (将数据表所有记录删除)
(4) 添加数据记录：
sql="insert into 数据表 (字段1,字段2,字段3 …) values (值1,值2,值3 …)"
sql="insert into 目标数据表 select * from 源数据表" (把源数据表的记录添加到目标数据表)
(5) 数据记录统计函数：
AVG(字段名) 得出一个表格栏平均值
COUNT(*;字段名) 对数据行数的统计或对某一栏有值的数据行数统计
MAX(字段名) 取得一个表格栏最大的值
MIN(字段名) 取得一个表格栏最小的值
SUM(字段名) 把数据栏的值相加
引用以上函数的方法：
sql="select sum(字段名) as 别名 from 数据表 where 条件表达式"
set rs=conn.excute(sql)
用 rs("别名") 获取统计的值，其它函数运用同上。
查询去除重复值：select distinct * from table1
(6) 数据表的建立和删除：
CREATE TABLE 数据表名称(字段1 类型1(长度),字段2 类型2(长度) …… )
(7) 单列求和:
SELECT SUM(字段名) FROM 数据表
```

### 列操作

```
查看列：desc 表名;
修改表名：alter table t_book rename to bbb;
添加列：alter table 表名 add column 列名 varchar(30);
删除列：alter table 表名 drop column 列名;
修改列名MySQL： alter table bbb change nnnnn hh int;
修改列名SQLServer：exec sp_rename't_student.name','nn','column';
修改列名Oracle：lter table bbb rename column nnnnn to hh int;
修改列属性：alter table t_book modify name varchar(22);
```


## Reference

1. [mysql和sqlserver中查看当前库中所有表和字段信息](http://www.cnblogs.com/Robotke1/archive/2013/04/24/3041372.html)
2. [mysql 列操作](http://blog.csdn.net/ws84643557/article/details/6939846)



