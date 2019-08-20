# synchronized 同步

在Java 中，每一个对象都有且仅有一个同步锁，即同步锁依赖对象而存在。当我们调用某对象的synchronized方法时，就获取了该对象的同步锁。不同线程对同步锁的访问是互斥的。synchronized 有以下三条原则：

- 当一个线程访问“某对象”的“synchronized方法”或者“synchronized代码块”时，其他线程对“该对象”的该“synchronized方法”或者“synchronized代码块”的访问将被阻塞。

- 当一个线程访问“某对象”的“synchronized方法”或者“synchronized代码块”时，其他线程仍然可以访问“该对象”的非同步代码块。

- 当一个线程访问“某对象”的“synchronized方法”或者“synchronized代码块”时，其他线程对“该对象”的其他的“synchronized方法”或者“synchronized代码块”的访问将被阻塞。

## 实例锁和全局锁

- 实例锁 synchronized ：锁在某一个实例对象上。

- 全局锁 static synchronized：锁针对的是类，无论实例多少个对象，线程将共享该锁。

## 重入锁

当一个线程得到一个对象后，再次请求该对象锁时是可以再次得到该对象的锁的。

具体概念就是：自己可以再次获取自己的内部锁。

Java里面内置锁(synchronized)和Lock(ReentrantLock)都是可重入的。

## 公平锁

公平锁可以保证线程按照时间的先后顺序执行，避免饥饿现象的产生。但公平锁的效率比较低，因为要实现顺序执行，需要维护一个有序队列。

synchronized控制的锁是非公平锁。

ReentrantLock通过在构造方法中传入true就是公平锁，传入false，就是非公平锁。