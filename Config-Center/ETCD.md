## etcd

网站：https://etcd.io/

GitHub地址： https://github.com/etcd-io/etcd

文档： https://github.com/etcd-io/etcd


> 是 CoreOS 基于 Raft 开发的分布式 key-value 存储，可用于服务发现、共享配置以及一致性保障（如数据库选主、分布式锁等）

### 目录
- [主要功能](#主要功能)


### 主要功能
- 基本的 key-value 存储
- 监听机制
- key 的过期及续约机制，用于监控和服务发现
- 原子 CAS 和 CAD，用于分布式锁和 leader 选举

可以做集群部署，服务注册中心。


