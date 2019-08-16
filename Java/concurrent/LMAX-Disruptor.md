## 并发框架 LMAX Disruptor

### 目录
- [JDK内置的内存消息队列](#JDK内置的内存消息队列)
- [Disruptor如何实现高性能](#Disruptor如何实现高性能)
- [Disruptor使用场景](#Disruptor使用场景)
- [使用步骤](#使用步骤)
- [核心概念](#核心概念)

Disruptor是英国外汇交易公司LMAX开发的一个高性能队列，研发的初衷是解决内存队列的延迟问题（在性能测试中发现竟然与I/O操作处于同样的数量级）。基于Disruptor开发的系统单线程能支撑每秒600万订单，2010年在QCon演讲后，获得了业界关注。2011年，企业应用软件专家Martin Fowler专门撰写长文介绍。同年它还获得了Oracle官方的Duke大奖。

- A High Performance Inter-Thread Messaging Library。一个高性能的线程间消息传递库。
- Disruptor是一个开源的并发框架，能够在无锁的情况下实现网络的Queue并发操作。
- Disruptor是一个高性能的异步处理框架，或者可以认为是最快的消息框架（轻量级JMS），也可以认为是一个观察者模式的实现，或者事件监听模式的实现。

### 常用线程安全的内置消息队列

<table>
    <tr><th>队列</th><th>加锁方式</th><th>是否有界</th><th>数据结构</th></tr>
    <tr><td>ArrayBlockingQueue</td><td>加锁</td><td>有界</td><td>ArrayList</td></tr>
    <tr><td>LinkedBlockingQueue</td><td>加锁</td><td>无界</td><td>LinkedList</td></tr>
    <tr><td>ConcurrentLinkedQueue</td><td>CAS</td><td>无界</td><td>LinkedList</td></tr>
    <tr><td>LinkedTransferQueue</td><td>CAS</td><td>无界</td><td>LinkedList</td></tr>
    <tr><td>PriorityBlockingQueue</td><td>加锁</td><td>无界</td><td>heap</td></tr>
    <tr><td>DelayQueue</td><td>加锁</td><td>无界</td><td>heap</td></tr>
</table>

我们知道CAS算法比通过加锁实现同步性能高很多，而上表可以看出基于CAS实现的队列都是无界的，而有界队列是通过同步实现的。在系统稳定性要求比较高的场景下，为了防止生产者速度过快，如果采用无界队列会最终导致内存溢出，只能选择有界队列。而有界队列只有ArrayBlockingQueue，该队列是通过加锁实现的，在请求锁和释放锁时对性能开销很大，这时候基于有界队列的高性能的Disruptor就应运而生。

### Disruptor如何实现高性能

1.	去掉了锁，采用CAS算法。

2.	内部通过环形队列实现有界队列。

3.	元素位置定位。数组长度2^n，通过位运算，加快定位的速度。

### Disruptor使用场景

1.	Log4j2 , Apache Storm

2.	使用多线程技术去创建基于任务的工作流。Disruptor能用来并行创建任务，同时保证多个处理过程的有序性，并且它是没有锁的。

3.	主要用于对性能要求高，延迟低的场景。

### 使用步骤

引入Jar包。com.lmax.disruptor
```text
<dependency>
  <groupId>com.lmax</groupId>
  <artifactId>disruptor</artifactId>
  <version>3.4.2</version>
</dependency>
```

1.	建立一个Event类。

2.	建立一个工厂Event类，用于创建Event类实例对象。

3.	建立一个事件监听事件类，用于处理数据（Event类）。

4.	测试代码：实例化Disruptor实例，配置参数，Disruptor实例绑定监听事件类，接收并处理数据。

5.	在Disruptor中，真正存储数据的核心叫做RingBuffer，我们通过Disruptor实例来拿到它，然后把数据生产出来，把数据加入到RingBuffer的实例对象中。

### 核心概念

- RingBuffer

    环形的缓冲区。曾经 RingBuffer 是 Disruptor 中的最主要的对象，但从3.0版本开始，环形缓冲区仅仅负责对通过 Disruptor 进行交换的数据（事件）进行存储和更新。在一些更高级的应用场景中，Ring Buffer 可以由用户的自定义实现来完全替代。

- Sequence

    Disruptor使用Sequences来识别特定组件的位置。每个消费者(事件处理器)都像Disruptor本身一样维护一个序列。大多数并发代码依赖于这些序列值的移动，因此序列支持AtomicLong的许多当前特性。实际上，这两个值之间唯一真正的区别是序列包含额外的功能，以防止序列和其他值之间的错误共享。

- Sequencer

    - Disruptor真正的核心。
    
    - 这个接口的两种实现（单生产者和多生产者）实现了所有用于在生产者和消费者之间准确快速的并发算法。

- SequenceBarrier

    序列屏障由序列器Sequencer生成，包含对来自序列器和任何依赖消费者的序列的主已发布序列的引用。它包含逻辑，以确定是否有任何事件可供使用者处理。

- WaitStrategy

    - 等待策略

    - 决定了一个消费者将如何等待事件Event被生产者放置到Disruptor中。

- Event

    从生产者到消费者过程中所处理的数据单元。

- EventProcessor

    用于处理Disruptor事件的主事件循环，并拥有使用者序列的所有权。

- EventHandler

    由用户实现并且代表了Disruptor中的一个消费者的接口。

- Producer

    由用户实现，它调用RingBuffer来插入事件（Event），在Disruptor中没有相应的实现代码，由用户实现。

