
# shadowsocks使用

## 安装 package

sudo apt-get update
sudo apt-get install python-pip python-m2crypto supervisor
sudo pip install shadowsocks


## Ubuntu 下安装

### shadowsocks配置文件

```
$ cat /etc/shadowsocks/config.json

{
"server":"0.0.0.0",
"server_port":123456,
"password":"123456",
"timeout":120,
"method":"rc4-md5"
}
```

### 安装和使用 supervisor

```
$ cat /etc/supervisor/conf.d/shadowsocks.conf

[program:shadowsocks]
command=ssserver -c /etc/shadowsocks/config.json
user=deploy
autostart=true
autorestart=true
redirect_stderr=true
redirect_stdout=true
stdout_logfile=/home/deploy/logs/%(program_name)s-out.log
stdout_logfile_maxbytes=100MB
stdout_logfile_backups=10
stderr_logfile=/home/deploy/logs/%(program_name)s-err.log
stderr_logfile_maxbytes=100MB
stderr_logfile_backups=10
```

```
$ sudo supervisorctl reload
$ sudo supervisorctl reread
$ sudo supervisorctl status
$ sudo supervisorctl start shadowsocks
$ sudo supervisorctl stop shadowsocks
$ sudo supervisorctl tail -f shadowsocks stdout
$ sudo supervisorctl tail -f shadowsocks stderr
```

如果不用 `supervisor`，直接使用下面的命令

```shell
$ sudo ssserver -c /etc/shadowsocks/config.json -d start
$ sudo ssserver -c /etc/shadowsocks/config.json -d stop
```

## 基于 docker 搭建 shadowsocks

```shell
$ docker pull oddrationale/docker-shadowsocks
$ docker run -d -p 55555:55555 --name ss oddrationale/docker-shadowsocks -s 0.0.0.0 -p 55555 -k 12345678 -m rc4-md5
```

## 其他

- 修改 sshd 默认的 22 端口

```
$ sudo vi /etc/ssh/sshd_config
$ service ssh restart
```

## 参考资料

- [科学上网之EC2搭建shadowsocks](http://blog.leanote.com/post/caidewu555@gmail.com/EC2%E6%90%AD%E5%BB%BAss)
- [Shadowsocks从零开始一站式翻墙教程](http://shadowsocks.blogspot.jp/2015/01/shadowsocks.html)
- [Docker + DigitalOcean + Shadowsocks 5分钟科学上网](http://liujin.me/blog/2015/05/27/Docker-DigitalOcean-Shadowsocks-5-%E5%88%86%E9%92%9F%E7%A7%91%E5%AD%A6%E4%B8%8A%E7%BD%91/index.html)
- [科学上网之 Shadowsocks 安装及优化加速 | Jark's Blog](http://wuchong.me/blog/2015/02/02/shadowsocks-install-and-optimize/)

