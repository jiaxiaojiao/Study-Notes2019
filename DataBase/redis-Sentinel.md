# Redis 的哨兵机制 

- [Redis集群](redis-Cluster.md)

## 哨兵的作用

1. 监控：监控主从是否正常

2. 通知：出现问题时，可以通知相关人员

3. 故障迁移：自动主从切换

4. 统一的配置管理：连接者询问sentinel取得主从的地址 

5. Raft算法核心: 可视图


## 什么是哨兵机制?

Redis的哨兵(sentinel) 系统用于管理多个 Redis 服务器,该系统执行以下三个任务:
- 监控(Monitoring): 哨兵(sentinel) 会不断地检查你的Master和Slave是否运作正常。
- 提醒(Notification):当被监控的某个 Redis出现问题时, 哨兵(sentinel) 可以通过 API 向管理员或者其他应用程序发送通知。
- 自动故障迁移(Automatic failover):当一个Master不能正常工作时，哨兵(sentinel) 会开始一次自动故障迁移操作,它会将失效Master的其中一个Slave升级为新的Master, 并让失效Master的其他Slave改为复制新的Master; 当客户端试图连接失效的Master时,集群也会向客户端返回新Master的地址,使得集群可以使用Master代替失效Master。

哨兵(sentinel) 是一个分布式系统,你可以在一个架构中运行多个哨兵(sentinel) 进程,这些进程使用流言协议(gossipprotocols)来接收关于Master是否下线的信息,并使用投票协议(agreement protocols)来决定是否执行自动故障迁移,以及选择哪个Slave作为新的Master.

每个哨兵(sentinel) 会向其它哨兵(sentinel)、master、slave定时发送消息,以确认对方是否”活”着,如果发现对方在指定时间(可配置)内未回应,则暂时认为对方已挂(所谓的”主观认为宕机” Subjective Down,简称sdown).

若“哨兵群”中的多数sentinel,都报告某一master没响应,系统才认为该master"彻底死亡"(即:客观上的真正down机,Objective Down,简称odown),通过一定的vote算法,从剩下的slave节点中,选一台提升为master,然后自动修改相关配置.

虽然哨兵(sentinel) 释出为一个单独的可执行文件 redis-sentinel ,但实际上它只是一个运行在特殊模式下的 Redis 服务器，你可以在启动一个普通 Redis 服务器时通过给定 --sentinel 选项来启动哨兵(sentinel).

哨兵(sentinel) 的一些设计思路和zookeeper非常类似



二.哨兵模式的配置修改

实现步骤:
1.拷贝到etc目录
```text
    cp sentinel.conf  /usr/local/redis/etc
```

2.修改sentinel.conf配置文件
```text
sentinel monitor mymast  192.168.110.133 6379 1  #主节点 名称 IP 端口号 选举次数
```

配置主服务器的密码(如没设置密码，可以省略) 
```text
sentinel auth-pass mymaster 123456
``` 
  
3. 修改心跳检测 5000毫秒
```text
sentinel down-after-milliseconds mymaster 5000
```

4. 做多多少合格节点
```text
sentinel parallel-syncs mymaster 2
```

5. 启动哨兵模式
```text
./redis-server /usr/local/redis/etc/sentinel.conf --sentinel &
```

6. 停止哨兵模式

注意：

1.当启动哨兵模式之后，如果你的master服务器宕机之后，哨兵自动会在从redis服务器里面 投票选举一个master主服务器出来；这个主服务器也可以进行读写操作！

2.如果之前宕机的主服务器已经修好，可以正式运行了。那么这个服务器只能进行读的操作，会自动跟随由哨兵选举出来的新服务器！

3.大家可以进入./redis-cli，输入info，查看你的状态信息；