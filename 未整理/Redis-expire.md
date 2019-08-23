# Redis 设置过期时间
redis通过expire命令来设置key的过期时间。

语法：redis.expire(key, expiration)

1. 在小于2.1.3的redis版本里，只能对key设置一次expire。redis2.1.3和之后的版本里，可以多次对key使用expire命令，更新key的expire time。

2. redis术语里面，把设置了expire time的key 叫做：volatile keys。 意思就是不稳定的key。

3. 如果对key使用set或del命令，那么也会移除expire time。尤其是set命令，这个在编写程序的时候需要注意一下。

4. redis2.1.3之前的老版本里，如果对volatile keys 做相关写入操作(LPUSH,LSET)，和其他一些触发修改value的操作时，redis会删除该key。 也就是说 ：

redis.expire(key,expiration);

redis.lpush(key,field,value);

redis.get(key) //return null

redis2.1.3之后的版本里面没有这个约束，可以任意修改。

redis.set(key,100);

redis.expire(key,expiration);

redis.incr(key)

redis.get(key)

//redis2.2.2 return 101; redis<2.1.3 return 1;


5. redis对过期键采用了lazy expiration：在访问key的时候判定key是否过期，如果过期，则进行过期处理。其次，每秒对volatile keys 进行抽样测试，如果有过期键，那么对所有过期key进行处理。