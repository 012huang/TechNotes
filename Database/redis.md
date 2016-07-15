
# redis使用

## [Installation](http://redis.io/download)
Download, extract and compile Redis with:

```shell
$ wget http://download.redis.io/releases/redis-3.0.6.tar.gz 
$ tar xzf redis-3.0.6.tar.gz 
$ cd redis-3.0.6 
$ make
```

The binaries that are now compiled are available in the src directory. Run Redis with:

```
$ src/redis-server
$ src/redis-server --port 6383 (指定端口)
```

You can interact with Redis unsing the built-in client:

```
$ src/redis-cli or $ redis-cli -p 6383 or $ redis-cli -h 10.205.24.53 -p 7361
redis> set foo bar 
OK 
redis> get foo 
"bar"
```

## Command
### 远程登陆redis

```
redis-cli -h 10.205.24.53 -p 7361
```

### 开启redis服务

```
redis-server /home/users/zhengkaitao/.jumbo/etc/redis.conf &
```

### 关闭服务

```
redis-cli shutdown
``` 
is most effective.

### alias

```
alias redstart='redis-server /usr/local/etc/redis/6379.conf'
alias redstop='redis-cli -h 127.0.0.1 -p 6379 shutdown'
```

## Reference
- http://stackoverflow.com/questions/6910378/how-can-i-stop-redis-server
- http://blog.csdn.net/love__coder/article/details/8272180

