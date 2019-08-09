## Java基础

### slf4j日志

打印多个参数的日志 logger.info("id:[{}], name:[{}]", id , name);

### JSON转换
```text
com.alibaba.fastjson.JSON
// List 转 JSON
String str = JSON.toJSONString(list);
// JSON 转 list
List<User> list = JSON.parseObject(str, new TypeReference<List<User>>(){});
List<User> list = JSON.parseArray(str, User.class);
```
### Java关键字

**volatile**

Java语言提供了一种稍弱的同步机制，即volatile变量，用来确保将变量的更新操作通知到其他线程。当把变量声明为volatile类型后，编译器与运行时都会注意到这个变量是共享的，因此不会将该变量上的操作与其他内存操作一起重排序。volatile变量不会被缓存在寄存器或者对其他处理器不可见的地方，因此在读取volatile类型的变量时总会返回最新写入的值。

在访问volatile变量时不会执行加锁操作，因此也就不会使执行线程阻塞，因此volatile变量是一种比sychronized关键字更轻量级的同步机制。

当对非 volatile 变量进行读写的时候，每个线程先从内存拷贝变量到CPU缓存中。如果计算机有多个CPU，每个线程可能在不同的CPU上被处理，这意味着每个线程可以拷贝到不同的 CPU cache 中。

而声明变量是 volatile 的，JVM 保证了每次读变量都从内存中读，跳过 CPU cache 这一步。

当一个变量定义为volatile之后，将具备两种特性：
1. 保证此变量对所有线程的可见性。volatile修饰的变量不允许线程内部缓存和重排序，即直接修改内存。所以对其他线程是可见的。
2. 禁止指令重排序。
	
volatile 性能：volatile 的读性能消耗与普通变量几乎相同，但是写操作稍慢，因为它需要在本地代码中插入许多内存屏障指令来保证处理器不发生乱序执行。

volatile不能保证具有原子性。

**synchronized**

- synchronized
    
    - 实例锁，对类的当前实例加锁，防止其他线程同时访问该实例的所有synchronized块。

	- 如果实例被锁，则该实例的所有同步方法全部被锁。
- static synchronized 

    - 类锁，控制类的所有实例的并发访问，限制多线程中该类的所有实例同时访问JVM中该类所对应的代码块。
	
	- 如果类被锁，则该类的所有同步方法全部被锁。
	
	- 实例锁和类锁之间互不干扰。

**transient**

transient修饰符仅适用于变量，不适用于方法和类。

在序列化时，如果我们不想序列化特定变量以满足安全约束，那么我们应该将该变量声明为transient。执行序列化时，JVM会忽略transient变量的原始值并将默认值保存到文件中。因此，transient意味着不要序列化。
