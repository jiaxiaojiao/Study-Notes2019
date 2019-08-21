# 线程

### 总结Thread类和Runnable接口

### 线程池

### 并发 CopyOnWrite
#### 并发包 并发处理

#### 多线程

### ThreadLocal
### threadLocal 与 数据库连接池
由于请求中的一个事务涉及多个DAO操作，而这些DAO中的Connection不能从连接池中获得。如果是从连接池中获得的话，两个DAO就用到了两个Connection，这样的话是没有办法完成一个事务的。
DAO中的Connection如果是从ThreadLocal中获得的话，那么这些DAO就会被纳入到同一个Connection之下。当然了，这样的话，DAO中就不能把Connection关闭，否则下一个使用者就不能用了。