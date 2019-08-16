## 阻塞队列

在Java中，BlockingQueue的接口位于java.util.concurrent 包中(在Java5版本开始提供)。

BlockingQueue即阻塞队列，它是基于ReentrantLock，依据它的基本原理，我们可以实现Web中的长连接聊天功能，当然其最常用的还是用于实现生产者与消费者模式

在Java中，BlockingQueue是一个接口，它的实现类有ArrayBlockingQueue、DelayQueue、 LinkedBlockingDeque、LinkedBlockingQueue、PriorityBlockingQueue、SynchronousQueue等，它们的区别主要体现在存储结构上或对元素操作上的不同，但是对于take与put操作的原理，却是类似的。

### 阻塞与非阻塞

### 方法

阻塞队列一共有四套方法分别用来进行insert、remove和examine，当每套方法对应的操作不能马上执行时会有不同的反应，下面这个表格就分类列出了这些方法：

<table>
    <tr><th> - </th><th>Throws Exception</th><th>Special Value</th><th>Blocks</th><th>Times Out</th></tr>
    <tr><td>Insert</td><td>add(o)</td><td>offer(o)</td><td>put(o)</td><td>offer(o, timeout, timeunit)</td></tr>
    <tr><td>Remove</td><td>remove(o)</td><td>poll()</td><td>take()</td><td>poll(timeout, timeunit)</td></tr>
    <tr><td>Examine</td><td>element()</td><td>peek()</td><td></td><td></td></tr>
</table>

这四套方法对应的特点分别是：
```text
1. ThrowsException：如果操作不能马上进行，则抛出异常
2. SpecialValue：如果操作不能马上进行，将会返回一个特殊的值，一般是true或者false
3. Blocks:如果操作不能马上进行，操作会被阻塞
4. TimesOut:如果操作不能马上进行，操作会被阻塞指定的时间，如果指定时间没执行，则返回一个特殊值，一般是true或者false
```
需要注意的是，我们不能向BlockingQueue中插入null，否则会报NullPointerException。

### 实现类

BlockingQueue只是java.util.concurrent包中的一个接口，而在具体使用时，我们用到的是它的实现类，当然这些实现类也位于java.util.concurrent包中。在Java8中，BlockingQueue的实现类主要有以下几种：

1. ArrayBlockingQueue
2. DelayQueue
3. LinkedBlockingDeque
4. LinkedBlockingQueue
5. LinkedTransferQueue
6. PriorityBlockingQueue
7. SynchronousQueue

下面我们就分别介绍这几个实现类。

#### ArrayBlockingQueue

ArrayBlockingQueue是一个有边界的阻塞队列，它的内部实现是一个数组。有边界的意思是它的容量是有限的，我们必须在其初始化的时候指定它的容量大小，容量大小一旦指定就不可改变。

ArrayBlockingQueue是以先进先出的方式存储数据，最新插入的对象是尾部，最新移出的对象是头部。

```text
BlockingQueue queue = new ArrayBlockingQueue(1024);
queue.put("1");
Object o = queue.take();
```

#### DelayQueue

DelayQueue阻塞的是其内部元素，DelayQueue中的元素必须实现 java.util.concurrent.Delayed接口，这个接口的定义非常简单：

```text
public interface Delayed extends Comparable<Delayed> {

    /**
     * Returns the remaining delay associated with this object, in the
     * given time unit.
     *
     * @param unit the time unit
     * @return the remaining delay; zero or negative values indicate
     * that the delay has already elapsed
     */
    long getDelay(TimeUnit unit);
}
```
getDelay()方法的返回值就是队列元素被释放前的保持时间，如果返回0或者一个负值，就意味着该元素已经到期需要被释放，此时DelayedQueue会通过其take()方法释放此对象。

从上面Delayed 接口定义可以看到，它还继承了Comparable接口，这是因为DelayedQueue中的元素需要进行排序，一般情况，我们都是按元素过期时间的优先级进行排序。

#### LinkedBlockingQueue

LinkedBlockingQueue阻塞队列大小的配置是可选的，如果我们初始化时指定一个大小，它就是有边界的，如果不指定，它就是无边界的。说是无边界，其实是采用了默认大小为Integer.MAX_VALUE的容量 。它的内部实现是一个链表。

和ArrayBlockingQueue一样，LinkedBlockingQueue 也是以先进先出的方式存储数据，最新插入的对象是尾部，最新移出的对象是头部。下面是一个初始化和使LinkedBlockingQueue的例子：

```text
BlockingQueue<String> unbounded = new LinkedBlockingQueue<String>();
BlockingQueue<String> bounded = new LinkedBlockingQueue<String>(1024);
bounded.put("Value");
String value = bounded.take();
```

#### PriorityBlockingQueue

PriorityBlockingQueue是一个没有边界的队列，它的排序规则和 java.util.PriorityQueue一样。需要注意，PriorityBlockingQueue中允许插入null对象。

所有插入PriorityBlockingQueue的对象必须实现 java.lang.Comparable接口，队列优先级的排序规则就是按照我们对这个接口的实现来定义的。

另外，我们可以从PriorityBlockingQueue获得一个迭代器Iterator，但这个迭代器并不保证按照优先级顺序进行迭代。

#### SynchronousQueue

SynchronousQueue队列内部仅允许容纳一个元素。当一个线程插入一个元素后会被阻塞，除非这个元素被另一个线程消费。