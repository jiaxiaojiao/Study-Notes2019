## synchronized与static synchronized的区别


- **synchronized** 实例锁，对类的**当前实例**进行加锁，防止其他线程同时访问该实例的所有synchronized块。

- **static synchronized** 类锁，控制**类的所有实例**的并发访问，限制多线程中该类的所有实例同时访问JVM中该类所对应的代码块。

#### 例题：

假如有Something类的两个实例x与y，那么下列各组方法被多线程同时访问的情况是怎样的？

```text
pulbic class Something{
    public synchronized void isSyncA(){}
    public synchronized void isSyncB(){}
    public static synchronized void cSyncA(){}
    public static synchronized void cSyncB(){}
}

A.  x.isSyncA() 与 x.isSyncB()   
B.  x.isSyncA() 与 y.isSyncA()  
C.  x.cSyncA() 与 y.cSyncB()  
D.  x.isSyncA() 与 Something.cSyncA()

```

A： 不能被同时访问，原因：是对相同实例x的不同synchronized域访问。

B： 可以被同时访问，原因：是对不同实例x和y的相同synchronized域访问。

C： 不能被同时访问，原因：是对不同实例x和y的不同static synchronized域访问。

D： 可以被同时访问，原因：是对实例x的synchronized域和类Something的static synchronized域同时访问。

#### 总结：
- synchronized锁的是实例对象，static synchronized锁的是类对象
- 若实例被锁，则该实例的所有同步方法全部被锁
- 若类被锁，则该类的所有同步方法全部被锁
- 实例锁与类锁之间互不干扰