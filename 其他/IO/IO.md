# IO

> 字节流操作类和字符流操作类组成了Java IO体系

## IO 常见类

#### 文件流：FileInputStream/FileOutputStream， FileReader/FileWriter

> 这四个类是专门操作文件流的，用法高度相似，区别在于前面两个是操作字节流，后面两个是操作字符流。它们都会直接操作文件流，直接与OS底层交互。因此他们也被称为节点流。

#### 包装流：PrintStream/PrintWriter/Scanner
> PrintStream可以封装（包装）直接与文件交互的节点流对象OutputStream, 使得编程人员可以忽略设备底层的差异，进行一致的IO操作。因此这种流也称为处理流或者包装流。

> PrintWriter除了可以包装字节流OutputStream之外，还能包装字符流Writer

> Scanner可以包装键盘输入，方便地将键盘输入的内容转换成我们想要的数据类型。

#### 字符串流：StringReader/StringWriter
> 这两个操作的是专门操作String字符串的流，其中StringReader能从String中方便地读取数据并保存到char数组，而StringWriter则将字符串类型的数据写入到StringBuffer中（因为String不可写）。

#### 转换流：InputStreamReader/OutputStreamReader
> 这两个类可以将字节流转换成字符流，被称为字节流与字符流之间的桥梁。我们经常在读取键盘输入(System.in)或网络通信的时候，需要使用这两个类

#### 缓冲流：BufferedReader/BufferedWriter ， BufferedInputStream/BufferedOutputStream
> 没有经过Buffered处理的IO， 意味着每一次读和写的请求都会由OS底层直接处理，这会导致非常低效的问题。

> 经过Buffered处理过的输入流将会从一个buffer内存区域读取数据，本地API只会在buffer空了之后才会被调用（可能一次调用会填充很多数据进buffer）。

> 经过Buffered处理过的输出流将会把数据写入到buffer中，本地API只会在buffer满了之后才会被调用。

> BufferedReader/BufferedWriter可以将字符流(Reader)包装成缓冲流，这是最常见用的做法。

> 另外，BufferedReader提供一个readLine()可以方便地读取一行，而FileInputStream和FileReader只能读取一个字节或者一个字符，

> 因此BufferedReader也被称为行读取器

####  总结上面几种流的应用场景：
```text
FileInputStream/FileOutputStream  需要逐个字节处理原始二进制流的时候使用，效率低下
FileReader/FileWriter 需要组个字符处理的时候使用
StringReader/StringWriter 需要处理字符串的时候，可以将字符串保存为字符数组
PrintStream/PrintWriter 用来包装FileOutputStream 对象，方便直接将String字符串写入文件 
Scanner　用来包装System.in流，很方便地将输入的String字符串转换成需要的数据类型
InputStreamReader/OutputStreamReader ,  字节和字符的转换桥梁，在网络通信或者处理键盘输入的时候用
BufferedReader/BufferedWriter ， BufferedInputStream/BufferedOutputStream ， 缓冲流用来包装字节流后者字符流，提升IO性能，BufferedReader还可以方便地读取一行，简化编程。
```

## [to...NIO](NIO.md) 

## IO 与 NIO 

IO | NIO 
---- | ----
面向流 | 面向缓冲
阻塞IO | 非阻塞IO
无 | 选择器

#### 1、面向流与面向缓冲
Java IO和NIO之间第一个最大的区别是，IO是面向流的，NIO是面向缓冲区的。 Java IO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方。此外，它不能前后移动流中的数据。如果需要前后移动从流中读取的数据，需要先将它缓存到一个缓冲区。 Java NIO的缓冲导向方法略有不同。数据读取到一个它稍后处理的缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。但是，还需要检查是否该缓冲区中包含所有您需要处理的数据。而且，需确保当更多的数据读入缓冲区时，不要覆盖缓冲区里尚未处理的数据。

#### 2、阻塞与非阻塞IO
Java IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。Java NIO的非阻塞模式，使一个线程从某通道发送请求读取数据，但是它仅能得到目前可用的数据，如果目前没有数据可用时，就什么都不会获取，而不是保持线程阻塞，所以直至数据变的可以读取之前，该线程可以继续做其他的事情。 非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以一个单独的线程现在可以管理多个输入和输出通道（channel）。

#### 3、选择器（Selectors）
Java NIO的选择器允许一个单独的线程来监视多个输入通道，你可以注册多个通道使用一个选择器，然后使用一个单独的线程来“选择”通道：这些通道里已经有可以处理的输入，或者选择已准备写入的通道。这种选择机制，使得一个单独的线程很容易来管理多个通道。

Java NIO: 单线程管理多个连接

Java IO: 一个典型的IO服务器设计- 一个连接通过一个线程处理.