# Redis

 ## Redis简介
> 本质上是一个key-value 的NoSQL非关系型数据库，内存数据库，整个数据库系统加载在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。

最新版本： 

    Redis 5.0.5     Released Wed May 15 17:57:41 CEST 2019

Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。 

它支持多种类型的数据结构，如 字符串（strings）， 散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets） 与范围查询， bitmaps， hyperloglogs 和 地理空间（geospatial） 索引半径查询。 

Redis 内置了 复制（replication），LUA脚本（Lua scripting）， LRU驱动事件（LRU eviction），事务（transactions） 和不同级别的 磁盘持久化（persistence）， 并通过 Redis哨兵（Sentinel）和自动 分区（Cluster）提供高可用性（high availability）。

## 安装Redis

> 默认端口6379

为什么选择6379作为默认端口：6379在手机按键上MERZ对应的号码，而MERZ取自意大利歌女Alessia Merz的名字。MERZ长期以来被antirez及其朋友当做愚蠢的代名词。


- [Linux下安装Redis](Redis-InstallL.md)

- [Windows下安装Redis](Redis-InstallW.md)

## 为什么要用Redis

**高性能**：从数据库访问数据比较慢（硬盘读取的），将数据存在Redis缓存中，下一次直接访问缓存，速度很快，因为是内存操作。如果数据库数据出现改变，同步改变缓存中响应的数据。

**高并发**：Redis缓存能承受的并发请求远大于数据库，减轻数据库压力。

## 为什么不用map做缓存

缓存分为本地缓存和分布式缓存。

本地缓存： 以Java为例，使用自带的 map 或者 guava 实现的是本地缓存。
    - 轻量以及快速，但数据存储有限。
    - 生命周期随着 jvm 的销毁而结束
    - 在多实例的情况下，每个实例都需要各自保存一份缓存，缓存不具有一致性。

分布式缓存： 使用 redis 或 memcached 之类的称为分布式缓存，
    - 持久化
    - 过期机制
    - 在多实例的情况下，各实例共用一份缓存数据，缓存具有一致性。
    - 缺点是需要保持 redis 或 memcached服务的高可用，整个程序架构上较为复杂

## Redis和Memcached的区别

1. 数据类型
    - Redis支持丰富的数据类型： 字符串（strings）， 散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets）
    - Memcached支持简单的数据类型： 文本型（String）、二进制类型（新版本加的）

2. 持久化
    - Redis支持持久化： 可以将内存中的数据保持在磁盘中。重启机器、机器故障之后恢复数据。
    - Memcached支持持久化： 把数据全部存在内存中。

3. 集群模式
    - Redis原生集群： Redis cluster模式
    - Memcached没有原生集群模式。

4. 网络IO模型
    - Redis 单线程，多路IO复用模型。 
    - Memcached 多线程，非阻塞IO复用的网络模型。


## Redis的优点和缺点

- 优点：
    - 纯内存操作，性能快。
    - 支持多种数据结构，单个value的最大限制是1GB
    - 支持事务，操作都是原子性的（对数据的更改要不全部执行，要不全部不执行）
    - 丰富的特性，可用于缓存，消息，按Key设置过期时间，过期自动删除。

- 缺点：
    - 数据库容量收物理内存限制
    - 不能用作海量数据的高性能读写

## Redis的数据类型

数据类型： 字符串（String）， 列表（List）， 集合（Set），有序集合（Sorted Set） ,散列（Hashes） 。

这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作。

Redis底层数据结构：

编码常量 | 编码所对应的底层数据结构
--- | ---
REDIS_ENCODING_INT | long 类型的整数
REDIS_ENCODING_EMBSTR | embstr 编码的简单动态字符串
REDIS_ENCODING_RAW | 简单动态字符串
REDIS_ENCODING_HT | 字典
REDIS_ENCODING_LINKEDLIST | 双端链表
REDIS_ENCODING_ZIPLIST | 压缩列表
REDIS_ENCODING_INTSET | 整数集合
REDIS_ENCODING_SKIPLIST | 跳跃表和字典



- 字符串 String 
    - 常用命令： set, get, decr, incr, mget
    - 描述： 常规key-value类型，value可以是String或数字。
    - 场景： 常规key-value缓存、微博数、粉丝数等。
    - 底层实现： 字符串对象的编码可以是int、raw或者embstr。
      - 如果一个字符串的内容可以转换为long，那么该字符串就会被转换成为long类型，对象的ptr就会指向该long，并且对象类型也用int类型表示。
      - 普通的字符串有两种，embstr和raw。embstr应该是Redis 3.0新增的数据结构,在2.8中是没有的。如果字符串对象的长度小于39字节，就用embstr对象。否则用传统的raw对象。
      - embstr的创建只需分配一次内存，而raw为两次。
      
    
- 散列 Hash
    - 常用命令： hget, hset, hgetall
    - 描述： 是一个String类型的field和value的映射表
    - 场景： 适合存储对象
    - 底层实现： 哈希对象的底层实现可以是ziplist或者hashtable。
        - ziplist中的哈希对象是按照key1,value1,key2,value2这样的顺序存放来存储的。当对象数目不多且内容不大时，这种方式效率是很高的。
        - hashtable的是由dict这个结构来实现的
            
            
    
- 列表 List 
    - 常用命令： lpush, rpush, lpop, rpop, lrange
    - 描述： 链表。可以实现双向链表，支持反向查找和遍历。
    - 场景： 微博关注列表，粉丝列表，消息列表，lrange命令实现分页查询。
    - 底层实现： 列表对象的编码可以是ziplist或者linkedlist。
        - ziplist是一种压缩链表，它的好处是更能节省内存空间，因为它所存储的内容都是在连续的内存区域当中的。当列表对象元素不大，每个元素也不大的时候，就采用ziplist存储。但当数据量过大时就ziplist就不是那么好用了。因为为了保证他存储内容在内存中的连续性，插入的复杂度是O(N)，即每次插入都会重新进行realloc。
        - linkedlist是一种双向链表。它的结构比较简单，节点中存放pre和next两个指针，还有节点相关的信息。当每增加一个node的时候，就需要重新malloc一块内存。      
    
- 集合 Set
    - 常用命令： sadd, spop, smembers, sunion
    - 描述： 类似于List的列表，特殊之处在于Set可以自动排序。可以基于 set 轻易实现交集、并集、差集的操作。
    - 场景： 微博关注人和粉丝，可以方便实现共同关注 共同粉丝等功能。
    - 底层实现： 集合对象的编码可以是intset或者hashtable。
        - intset是一个整数集合，里面存的为某种同一类型的整数，支持如下三种长度的整数：
        ```text
        #define INTSET_ENC_INT16 (sizeof(int16_t))  
        #define INTSET_ENC_INT32 (sizeof(int32_t))  
        #define INTSET_ENC_INT64 (sizeof(int64_t))
        ```
        - intset是一个有序集合，查找元素的复杂度为O(logN)，但插入时不一定为O(logN)，因为有可能涉及到升级操作。比如当集合里全是int16_t型的整数，这时要插入一个int32_t，那么为了维持集合中数据类型的一致，那么所有的数据都会被转换成int32_t类型，涉及到内存的重新分配，这时插入的复杂度就为O(N)了。是intset不支持降级操作。

- 有序集合 Sorted Set ZSet
    - 常用命令： zadd, zrange, zrem, zcard
    - 描述： 和set相比，sorted set增加了一个权重参数score，使得集合中的元素能够按score进行有序排列。
    - 场景： 在直播系统中，实时排行信息包含直播间在线用户列表，各种礼物排行榜，弹幕消息（可以理解为按消息维度的消息排行榜）等信息，适合使用 Redis 中的 Sorted Set 结构进行存储。
    - 底层实现： 有序集合的编码可能两种，一种是ziplist，另一种是skiplist与dict的结合。
        - ziplist作为集合和作为哈希对象是一样的，member和score顺序存放。按照score从小到大顺序排列。它的结构不再复述。
        - skiplist是一种跳跃表，它实现了有序集合中的快速查找，在大多数情况下它的速度都可以和平衡树差不多。但它的实现比较简单，可以作为平衡树的替代品。它的结构比较特殊。
        - 为什么要用这种结构呢。试想如果单一用hashtable，那可以快速查找、添加和删除元素，但没法保持集合的有序性。如果单一用skiplist，有序性可以得到保障，但查找的速度太慢O（logN），hashtable用于查找。

### Redis设置过期时间
语法：redis.expire(key, expiration)

set key 的时候，都可以给一个 expire time。

Redis是怎么删除已经设置过期时间的Key的？
- 定期删除： redis默认是每隔 100ms 就**随机抽取**一些设置了过期时间的key，检查其是否过期，如果过期就删除。注意这里是随机抽取的。
- 惰性删除： 定期删除可能会导致很多过期 key 到了时间并没有被删除掉。所以就有了惰性删除。假如你的过期 key，靠定期删除没有被删除掉，还停留在内存里，除非你的系统去查一下那个 key，才会被redis给删除掉。


如果定期删除漏掉了很多过期 key，然后你也没及时去查，也就没走惰性删除，此时会怎么样？如果大量过期key堆积在内存里，导致redis内存块耗尽了。怎么解决这个问题呢？ **redis 内存淘汰机制。**

## Redis数据淘汰机制

在redis中允许用户设置最大使用内存大小server.maxmemory。内存大小有限，需要保存有效的数据。

redis内存数据集大小上升到一定大小时，就会实施数据淘汰策略/回收策略。

Redis提供了6中数据淘汰策略。
1. volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰。
2. volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰 。
3. volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰 。
4. allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰 。
5. allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰 。
6. no-enviction（驱逐）：禁止驱逐数据。

4.0版本后增加以下两种：

7. **volatile-lfu**：从已设置过期时间的数据集(server.db[i].expires)中挑选最不经常使用的数据淘汰
8. **allkeys-lfu**：当内存不足以容纳新写入数据时，在键空间中，移除最不经常使用的key


## 拓展
- [Redis 的常见应用场景](Redis-Context-of-Use.md)
- [Redis 的并发竞争问题](Redis-Concurrent.md)
- [Redis 的哨兵机制](Redis-Sentinel.md)
- [Redis 的集群部署](Redis-Cluster.md)
- [RedLock 分布式锁](Redis-RedLock.md)
- [Redis 事务](Redis-Transaction.md)
- [Redis 缓存](Redis-Cache.md)
- [Java使用RedisTemplate](Redis-Template.md)
- 《Redis实战》


## Redis常见面试题
- [redis 简介](#Redis简介)
- [为什么要用 redis/为什么要用缓存](#为什么要用Redis)
- [为什么要用 redis 而不用 map/guava 做缓存?](#为什么不用map做缓存)
- [redis 和 memcached 的区别](#Redis和Memcached的区别)
- [redis 常见数据结构以及使用场景分析](#Redis的数据类型)
    - String
    - Hash
    - List
    - Set
    - Sorted Set
- [redis 设置过期时间](#Redis设置过期时间)
- [redis 内存淘汰机制(MySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据?)](#Redis数据淘汰机制)
- [redis 持久化机制/存储策略(怎么保证 redis 挂掉之后再重启数据可以进行恢复)](Redis-Persistence.md)
- [缓存雪崩和缓存穿透问题解决方案](Redis-Cache.md)
- [如何解决 Redis 的并发竞争 Key 问题](Redis-Concurrent.md)
- [如何保证缓存与数据库双写时的数据一致性?](Redis-Cache.md)
