# 线程
```text
package java.lang;
public class Thread implements Runnable {}
```

## 线程的实现方式

#### 1. 通过继承Thread类实现一个线程

```text
public class MyThread extends Thread{
    @Override
    public void run(){
        super.run();
    }
}
```


#### 2. 通过实现Runnable接口实现一个线程

推荐！
继承扩展性不强，Java支持单继承，继承了Thread就不能继承其它的类了。


## 启动线程
Thread thread = new Thread(new MyThread 继承了Thread的对象或者实现了Runnable的对象);

thread.start();

启动线程使用start方法，启动以后执行的是run方法。

## 区分线程

在系统中有很多线程，每个线程都会打印日志，我想区分哪个线程，
thread.setName("设置一个线程名称")
规范，在创建线程完成后，需要设置线程名称。


## 线程池/线程并发库
> JDK1.5增加的

> java.util.current包提供了对线程优化 管理的各项操作。

Java通过Executors提供了四个静态方法创建线程池：
1. newCachedThreadPool 创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则创建新线程。
2. newfixedThreadPool 创建一个定长线程池，可控制线程最大并发量，超出的线程会在队列中等待。
3. newScheduledThreadPool 创建一个定长线程池，支持定时及周期性任务执行。
4. newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序（FIFO,LIFO,优先级）执行。

线程池的作用？
1. 限定线程的个数，不会由于线程过多，导致系统运行缓慢或崩溃。
2. 线程池不需要每次都去创建或销毁，节约了资源。
3. 响应时间更快。

## 并发容器 CopyOnWrite
CopyOnWrite思路是在更改容器时，把容器写一份进行修改，保证正在读的线程不受影响，适合应用在读多写少的场景，因为写的时候重建一次容器。

#### 并发包 并发处理

## 线程局部变量 ThreadLocal
线程局部变量是局限于线程内部的变量，属于线程本身所有，不在多个线程间共享。Java提供ThreadLocal类来支持线程局部变量，是一种实现线程安全的方式。使用线程局部变量是注意： 工作线程的生命周期比任何应用变量的生命周期都要长，任何线程局部变量一旦在工作完成后没有释放，Java应用就存在内存泄露的风险。

#### threadLocal 与 数据库连接池
由于请求中的一个事务涉及多个DAO操作，而这些DAO中的Connection不能从连接池中获得。如果是从连接池中获得的话，两个DAO就用到了两个Connection，这样的话是没有办法完成一个事务的。

DAO中的Connection如果是从ThreadLocal中获得的话，那么这些DAO就会被纳入到同一个Connection之下。当然了，这样的话，DAO中就不能把Connection关闭，否则下一个使用者就不能用了。
     

## [多线程](Thread-multithreading.md) 
