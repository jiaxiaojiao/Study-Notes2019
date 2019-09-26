# Linux下安装Redis

### 1. 安装步骤
``` text
1、推荐进入到linux路径/usr/local/src
2、$ 
wget http://download.redis.io/releases/redis-4.0.10.tar.gz
3、$ tar xzf redis-4.0.10.tar.gz 
4、$ cd redis-4.0.10/ 
5、$ make
```

### 2. 启动Redis服务
``` text
二进制文件是编译完成后在src目录下，通过下面的命令启动Redis服务
$ src/redis-server

$ src/redis-cli
redis> set foo bar
OK
redis> get foo
"bar"
```

### 3. 配置， 修改配置文件
```text
- #bind 127.0.0.1  将这里前面加上#否则远程无法连接redis或者只能连接ip为127.0.0.1的本地回环地址，无法连接真实的ip.

- daemonize yes   （这里讲原来的no改为yes,目的是为了设置后台运行）

- protected-mode no  （这里讲原来的yes改为no,目的是为了解决安全模式引起的报错）
```


### 4. 移动redis的配置文件

1、在etc里面建立一个文件夹
   mkdir  /etc/redis
   注意：权限问题777
2、移动配置文件到新建的文件夹下
   cp  redis.conf  /etc/redis/
### 5. 杀死redis并重新后台开启redis

pkill -9 redis-server
src/redis-server /etc/redis/redis.conf

### 6. 检测redis是否开启

ps axu | grep redis-server

如果是最新时间开启的redis，则表明开启成功

### 7. 客户端远程通过ip连接redis


src/redis-cli -h 192.168.1.81 -p 6379

如果出现如下，则表明连接成功

192.168.1.81:6379>