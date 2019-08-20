# 集合

![image](images/collection.png)


```text
Collection 存储Value
|-- List 接口：有序集合，可以包含重复元素，可以按索引访问
    |-- ArrayList 底层使用数组，非线程安全，扩容每次对size增加50%
    |-- Vector 底层使用数组，线程安全，synchronize同步，性能较差。
    |-- LinkedList 底层使用双向链表(JDK1.6之前为循环链表，JDK1.7取消了循环)，非线程安全
|-- Set 接口：无序集合，不允许重复元素，根据equals和hashcode来判断唯一。
    |-- HashSet 底层使用数组+链表，非线程安全，基于HashMap实现。
    |-- LinkedHashSet 底层使用数组+链表，基于LinkedHashMap实现
    |-- TreeSet 底层使用红黑树，有序（默认升序），非线程安全

Map 接口：存储键值对 Key-Value，Key不允许重复。
|-- HashMap 底层使用数组+链表/红黑树，非线程安全，Key/Value允许为null
|-- TreeMap 底层使用红黑树，非线程安全，根据key排序，默认升序。
|-- HashTable 底层使用数组+链表，线程安全，继承Dictionary，Key/Value不允许为null。
|-- LinkedHashMap 继承自HashMap，增加了双向链表，保存了记录的插入顺序，非线程安全
|-- ConcurrentHashMap 底层使用数组+链表/红黑树，线程安全，无序

```

## List
ArrayList：
- 底层： 使用数组，内存中开辟一块连续的空间来存储，数据存储是连续的，支持下标来访问元素。
- 非线程安全
- 扩容： 更多元素添加进来时会请求更大的空间，每次对size增长50%。
- 场景： 在查询多，插入删除比较少的场景。

Vector：
- 底层： 使用数组
- 线程安全。所有的方法都是同步的。

LinkedList：
- 底层： 使用双向链表
- 场景： 使用在查询少，插入删除比较多的场景。

## Set
[TreeSet](Set-TreeSet.md):
- 底层： 红黑树
- 有序，默认升序。


## Map

[HashMap](Map-HashMap.md)：
- 底层： 数组+链表/红黑树
- Key和Value都允许空，只允许一条Key为null，允许多条记录的Value为null。
- Key：实际开发过程中key值基本都是String类型的。
- 非线程安全，效率较高。
- 实现HashMap的同步：Map m = Collections.synchronizedMap(new HashMap()) 
- 无序

[TreeMap](Map-TreeMap.md)：
- 底层： 红黑树。
- Key不允许为null
- 非线程安全
- 排序：根据key排序,默认是按升序排序。也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。

HashTable：
- 底层： 数组+链表。 数组是主体，链表主要是为了解决哈希冲突。
- Key/Value不允许为null。
- 继承Dictionary，线程安全，效率慢。

[LinkedHashMap](Map-LinkedHashMap.md):
- 继承自HashMap
- 底层： 数组+链表/红黑树 
- 增加了双向链表，保存了记录的插入顺序。
- Key和Value都允许空
- 非线程安全

ConcurrentHashMap：
- 底层： 数组+链表/红黑树
- 线程安全
- 无序

 
## 拓展
- [ArrayList 的 subList 使用注意事项](List-ArrayList.md#1-arraylist中的sublist)
 
- [有序集合对比 ArrayList LinkedList Vector](List-ArrayList.md#2-对比-arraylist和linkedlist-vector)

- **1.7版本和1.8版本的ConcurrentHashMap的区别**

  **1.8之后的ConcurrentHashMap**： 
  1. 取消 segments 字段，直接采用 transient volatile HashEntry<K,V>[] table保存数据，采用table数组元素作为锁，从而实现了对每一行数据进行加锁，进一步减少并发冲突的概率。
  2. 数组结构： 数组+链表+红黑树。
  3. 效率高
  
- Map相关方法的底层实现原理
  - Map底层实现的基础是数组和链表，通过数组的方式存储Map的每个元素。
  - 新增 put(Object key, Object value) ，新创建的Map对象设置为myMap数组的最后一个，让数组的长度加一。
  - 查找 get(Object key) ，通过对存储Map对象的数组的遍历，找到key值，然后返回Value。
  - key可以是任意类型，实际开发过程中key值基本都是String类型的，基本数据类型，引用数据类型。
