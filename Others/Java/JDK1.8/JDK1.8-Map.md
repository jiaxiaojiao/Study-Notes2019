# JDK 1.8 对Map的更新

JDK1.8 Java集合中新增的方法

接口名 | Java8新加入的方法
---|---
Collection | removeIf() spliterator() stream() parallelStream() forEach()
List | replaceAll() sort()
Map | getOrDefault() forEach() replaceAll() putIfAbsent() remove() replace() computeIfAbsent() computeIfPresent() compute() merge()

这些新加入的方法大部分要用到java.util.function包下的接口

## 红黑树
> 对HashMap等Map集合的数据结构优化。更快捷。

## [HashMap](../Collection/Map-HashMap.md) 

#### 原来的HashMap
1. 数据结构哈希表（数组+链表）
2. 默认大小 16
3. 达到总容量的0.75，数组扩容。
4. 存储元素，首先计算hashcode，计算数组的索引值，对应索引没有元素直接添加，有元素equals比较内容如果相等就覆盖 不相等后加的放在前面。
5. 效率低


#### 1.8之后的HashMap
1. 数据结构：数组+链表+红黑树
2. 碰撞元素>8 & 总容量大于64，引入红黑树。
3. 末尾插入。
4 效率高。
