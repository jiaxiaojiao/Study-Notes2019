


## hashCode
```text
① 一种算法，并不是完全唯一。
② 让同一个类的对象按照自己不同的特征尽量的有不同的哈希码。
③ 包含容器类型的程序设计语言，基本上都会涉及到hashCode。
④ Java  hashCode方法的主要作用是为了配合基于散列的集合一起正常运行 （HashSet、HashMap、 HashTable）
hashCode方法的存在是为了减少equals方法的调用次数，从而提高程序效率。
⑤ equals() 相等的两个对象， hashCode相等；
equals() 不相等的两个对象，hashCode有可能相等。
hashCode不等 =>  equals() 不等
hashCode相等 =>  equals() 可能相等
```

## instanceof
```text
左边对象是否是右边类的实例（左边对象是否是右边类或者是它的子类的一个实例）

用法：
result = Object instanceof class
参数：
result 布尔类型
Object 任意对象表达式
Class 任意已定义的对象类

如果Object不为null 并且(class)Object不抛ClassCastException异常则该表达式的值为true，否则值为false
```