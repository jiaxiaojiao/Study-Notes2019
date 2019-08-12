## Redis

### Redis的特点：

单线程工作模型。
	
### Redis和Memcached有什么区别？

1. 数据结构

    Redis支持复杂的数据结构。

2. 集群模式

    Redis3.0x版本后，支持原生cluster模式。
	
	Memcached没有原生的集群模式，需要依靠客户端来实现往集群中分片写入数据。

3. 性能
    
    Redis使用单核，存储小数据性能更高。
	
	Memcached使用多核，大数据存储Memcached性能更好。

### Redis的线程模型是什么？

Redis内部使用文件事件处理器file event handler，这个文件事件处理器是单线程的，所以Redis是单线程的模型。

采用IO多路复用机制同时监听多个socket，根据socket上的事件来选择对应的事件处理器进行处理。

文件事件处理器的结构，包含4个部分：
- 多个socket
- IO多路复用程序
- 文件事件分派器
- 事件处理器（连接应答处理器，命令请求处理器，命令回复处理器）

多个socket可能会并发产生不同的操作，每个操作对应不同的文件事件，但是IO多路复用程序会监听多个socket，会将socket产生的事件放入队列中，时间分派器每次从队列中取出一个事件，把该事件交给对应的事件处理器进行处理。

### 为什么Redis单线程却能支撑高并发？

- 纯内存操作

- 核心是基于非阻塞IO多路复用机制

- 单线程工作模型，避免了多线程的频繁上下文切换问题。

### Redis常用集群方案

**Redis主从方案**

Redis主从模式是最简单的一种集群方案配置起来也比较简单，它的特点主要有：
- 一个master可以拥有多个slave
- 多个slave链接同一个master，也可以链接其它slave
- 主从复制不会阻塞master,在同步数据时，master可以继续处理client请求.
- slave 配置为slave-read-only on需要升级为主节点或者写入配置文件中, 而不能在默认slave情况下直接设置master与slave断开后会检测心跳, 从新建立连接.
- 可以直接copy DUMP文件从新重启master，在Master为空以后，slave同步数据会抹掉全部数据.

**Redis Cluster方案**

Redis Cluster是一种服务器Sharding技术，3.0版本开始正式提供。

Redis Cluster中，Sharding采用slot(槽)的概念，一共分成16384个槽。对于每个进入Redis的键值对，根据key进行Hash，分配到这16384个slot中的某一个中。

Redis集群中的每个node(节点)负责分摊这16384个slot中的一部分。当动态添加或减少node节点时，需要将16384个槽做个再分配，槽中的键值也要迁移。

Redis集群，要保证16384个槽对应的node都正常工作，如果某个node发生故障，那它负责的slots也就失效，整个集群将不能工作。

为了增加集群的可访问性，官方推荐的方案是将node配置成主从结构，即一个master主节点，挂n个slave从节点。这时，如果主节点失效，Redis Cluster会根据选举算法从slave节点中选择一个上升为主节点，整个集群继续对外提供服务，Redis Cluster本身提供了故障转移容错的能力。

Redis Cluster的新节点识别能力、故障判断及故障转移能力是通过集群中的每个node都在和其它nodes进行通信，这被称为集群总线(cluster bus)。它们使用特殊的端口号，即对外服务端口号加10000。例如如果某个node的端口号是6379，那么它与其它nodes通信的端口号是16379。nodes之间的通信采用特殊的二进制协议。

对客户端来说，整个cluster被看做是一个整体，客户端可以连接任意一个node进行操作，就像操作单一Redis实例一样，当客户端操作的key没有分配到该node上时，Redis会返回转向指令，指向正确的node。

优点： 这种cluster的方案对比第一种简单的主从方案的优点在于提高了读写的并发，分散了IO，在保障高可用的前提下提高了性能。

**Codis集群方案**

Codis是一个豌豆荚团队开源的使用Go语言编写的Redis Proxy使用方法和普通的redis没有任何区别，设置好下属的多个redis实例后就可以了，使用时在本需要连接redis的地方改为连接codis，它会以一个代理的身份接收请求 并使用一致性hash算法，将请求转接到具体redis，将结果再返回codis，和之前比较流行的twitter开源的Twemproxy功能类似，但是相比官方的redis cluster和twitter的Twemproxy还是有一些独到的优势。

Codis一个比较大的优点是可以不停机动态新增或删除数据节点，旧节点的数据也可以自动恢复到新节点。并且提供图形化的dashboard，方便集群管理。

Codis方案推出的时间比较长，而且国内很多互联网公司都已经使用了该集群方案，所以该方案还是比较适合大型互联网系统使用的，毕竟成功案例比较多，但是codis因为要实现slot切片，所以修改了redis-server的源码，对于后续的更新升级也会存在一定的隐患。但是codis的稳定性和高可用确实是目前做的最好的，只要有足够多的机器能够做到非常好的高可用缓存系统。

总结：
	从各个集群方案的对比中我们也发现Codis是目前用的比较多的一种方案，Codis在高可用方面做的比较好，不需要重启节点和增加删除节点后自动Resharding，但是因为Codis是对redis-server做了改动，如果出现问题或者redis升级小团队可能应付不了，所以对于小规模应用最好还是使用官方的cluster方案，在redis3.0后官方社区也在逐步完善cluster方案，小团队可以随着官方版本的升级享受功能和稳定性的提升，也便于日后的维护。


### 为了达到Redis的高可用性，有两种部署方式：

1. 主从复制 + 哨兵机制（Redis2.8开始支持）

2. 集群模式 （Redis3.0开始支持）

**主从复制**

把主节点的数据复制给从节点。

从节点的作用：

1. 可以备份主节点的数据，如果主节点down了 可以接替主节点的工作。

2. 可用分担主节点读压力

没有哨兵机制的时候，主节点down了，主从切换需要人工介入。

**哨兵机制主要功能：**

1. 监控。 监控主从节点是否正常运行。

2. 提醒。 如果Redis运行出现异常，按照配置项通知客户端或集群管理员。

3. 自动故障转移。当主节点下线后，哨兵可以从主节点的多个从节点中选出一个为主节点，并更新配置文件和其他从节点的主节点信息。

**哨兵机制实现步骤：**
	
	1. 配置主节点的IP，Port，授权密码等
	   /usr/local/redis/etc sentinel.conf 
	2. 启动哨兵
	   /usr/local/redis/bin/redis-server /usr/local/redis/etc/sentinel.conf --sentinel &
	3. 查看哨兵信息
	   /usr/local/redis/bin/redis-cli -h 192.168.2.105 -p 26379 info Sentinel
	测试： 
	关闭master，查看集群信息（之前从节点中，变成主节点）
	# master 执行下面的命令
	/usr/local/redis/bin/redis-cli shutdown
	再次启动，查看集群信息（变成从节点）

[**返回首页目录**](README.md)