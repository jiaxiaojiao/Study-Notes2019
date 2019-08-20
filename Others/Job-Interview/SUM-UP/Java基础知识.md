## Java基础知识

#### Java和C++的区别
- 都是面向对象的语言，都支持封装、继承和多态。
- Java不提供指针来直接访问内存，程序内存更加安全。
- Java的类是单继承的，C++支持多重继承；虽然Java的类不可以多继承，但是接口可以多继承。
- Java有自动内存管理机制，不需要程序员手动释放无用内存

#### 1. 栈和队列
```text
栈和队列的数据类型： 
相同的： 都允许在端点插入和删除元素。
不同点： 栈只在栈顶访问，遵循后进先出原则（LIFO）；队列是在队尾插入数据，在队头删除数据（FIFO）

```

#### 2. 接口和抽象类
```text
抽象类： 含有抽象方法，用abstract修饰。继承关系。
接口interface：供别人调用的方法和函数。实现。接口中的方法都是抽象方法。实现接口使用implements。
抽象方法： 只有声明，没有具体实现。abstract void fun()

```

接口和抽象类的区别： 
- 接口的方法默认是public，所有方法在接口中不能有实现，抽象类可以有非抽象的方法
- 接口中的实例变量默认是final类型的，而抽象类中则不一定
- 一个类可以实现多个接口，但最多只能实现一个抽象类
- 一个类实现接口的话要实现接口的所有方法，而抽象类不一定
- 接口不能用new实例化，但可以声明，但是必须引用一个实现该接口的对象 从设计层面来说，抽象是对类的抽象，是一种模板设计，接口是行为的抽象，是一种行为的规范。



#### 3. int和Integer的
```text
int是基本数据类型。存数据值。 默认0
Integer是int的包装类。 实例化后才可以使用。new Integer是生成一个指针指向这个对象。默认null

```
#### 4. 自动拆箱/装箱
```text
自动装箱
用基本类型的值给它的包装类型赋值时，系统会自动将基本类型转成它的包装类型。

自动拆箱
当需要基本类型的时候，系统会自动将包装类型转成基本类型。

```

#### 5. 常量池
```text
分为两种： 静态常量池 / 运行时常量池

静态常量池： class文件中的常量池：字符串 类和方法。
运行时常量池： class文件被加载进内存之后，常量池保存在了方法区。 通常说的常量池，是运行时常量池。 

好处： 
1. 避免频繁的创建和销毁对象而影响系统性能。
2. 实现了对象的共享

```

#### 6. == 和equals

- ==

    它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象。(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)

- equals()

    它的作用也是判断两个对象是否相等。但它一般有两种使用情况：
    
    1. 类没有覆盖equals()方法。则通过equals()比较该类的两个对象时，等价于通过“==”比较这两个对象。
    2. 类覆盖了equals()方法。一般，我们都覆盖equals()方法来两个对象的内容相等；若它们的内容相等，则返回true(即，认为这两个对象相等)。
    
#### 为什么重写equals时必须重写hashCode方法？

hashCode()介绍： hashCode() 的作用是获取哈希码，也称为散列码；它实际上是返回一个int整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。hashCode() 定义在JDK的Object.java中，这就意味着Java中的任何类都包含有hashCode() 函数。另外需要注意的是： Object 的 hashcode 方法是本地方法，也就是用 c 语言或 c++ 实现的，该方法通常用来将对象的 内存地址 转换为整数之后返回。

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

为什么要有hashCode？ 

我们以“HashSet如何检查重复”为例子来说明为什么要有hashCode：

当你把对象加入HashSet时，HashSet会先计算对象的hashcode值来判断对象加入的位置，同时也会与其他已经加入的对象的hashcode值作比较，如果没有相符的hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同hashcode值的对象，这时会调用equals（）方法来检查hashcode相等的对象是否真的相同。如果两者相同，HashSet就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。（摘自我的Java启蒙书《Head fist java》第二版）。这样我们就大大减少了equals的次数，相应就大大提高了执行速度。

hashCode（）与equals（）的相关规定
- 如果两个对象相等，则hashcode一定也是相同的
- 两个对象相等,对两个对象分别调用equals方法都返回true
- 两个对象有相同的hashcode值，它们也不一定是相等的

因此，equals方法被覆盖过，则hashCode方法也必须被覆盖

hashCode()的默认行为是对堆上的对象产生独特值。如果没有重写hashCode()，则该class的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）    


#### 7. 重载和重写

- 重载: 同一个类中，方法名相同，参数不同，方法返回值和访问修饰符可以不同，发生在编译时。
- 重写:   父子类之间，方法名相同，参数相同。返回值范围小于等于父类，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类；如果父类方法访问修饰符为private则子类就不能重写该方法。



#### 8. String 和 StringBuffer ，StringBuilder的区别

- 【可变性】

    简单的来说：String 类中使用 final 关键字字符数组保存字符串，private　final　char　value[]，所以 String 对象是不可变的。而StringBuilder 与 StringBuffer 都继承自 AbstractStringBuilder 类，在 AbstractStringBuilder 中也是使用字符数组保存字符串char[]value 但是没有用 final 关键字修饰，所以这两种对象都是可变的。

    StringBuilder 与 StringBuffer 的构造方法都是调用父类构造方法也就是 AbstractStringBuilder 实现的。
    ```text
    AbstractStringBuilder.java
    abstract class AbstractStringBuilder implements Appendable, CharSequence {
        char[] value;
        int count;
        AbstractStringBuilder() {
        }
        AbstractStringBuilder(int capacity) {
            value = new char[capacity];
        }
    }    
    ```

- 【线程安全性】
    
    String 中的对象是不可变的，也就可以理解为常量，线程安全。
    
    AbstractStringBuilder 是 StringBuilder 与 StringBuffer 的公共父类，定义了一些字符串的基本操作，如 expandCapacity、append、insert、indexOf 等公共方法。
    
    StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。
    
    StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的。

- 【性能】
    
    每次对 String 类型进行改变的时候，都会生成一个新的 String 对象，然后将指针指向新的 String 对象。StringBuffer 每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 StirngBuilder 相比使用 StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。
    
    String < StringBuffer < StringBuilder

对于三者使用的总结：
1. 操作少量的数据 = String
2. 单线程操作字符串缓冲区下操作大量数据 = StringBuilder
3. 多线程操作字符串缓冲区下操作大量数据 = StringBuffer


#### 成员变量与局部变量的区别有那些？
- 从语法形式上，看成员变量是属于类的，而局部变量是在方法中定义的变量或是方法的参数；成员变量可以被public,private,static等修饰符所修饰，而局部变量不能被访问控制修饰符及static所修饰；但是，成员变量和局部变量都能被final所修饰；
- 从变量在内存中的存储方式来看，成员变量是对象的一部分，而对象存在于堆内存，局部变量存在于栈内存
- 从变量在内存中的生存时间上看，成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动消失。
- 成员变量如果没有被赋初值，则会自动以类型的默认值而赋值（一种情况例外被final修饰但没有被static修饰的成员变量必须显示地赋值）；而局部变量则不会自动赋值。
      
#### 双向链表和双向循环链表？

双向链表：包含两个指针，一个prev指向前一个节点，一个next指向后一个节点。

双向循环链表： 最后一个节点的 next 指向head，而 head 的prev指向最后一个节点，构成一个环。

