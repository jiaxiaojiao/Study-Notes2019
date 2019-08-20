# Java 基础 - 字符串String 

## String, StringBuffer，StringBuilder的区别

- String 

    不可变，final。

- StringBuffer 

    可变。

    线程安全。

- StringBuilder

    可变。

    非线程安全。
    
## 比较字符串

String内部实现了Comparable接口。

有两个比较方法：compareTo 和compareToIgnoreCase（相当于使用了大小写转换再比较）

## 字符串编程小写形式/大写形式

使用toUpperCase 和 toLowerCase 方法让一个字符串变为 大写或小写。

## 字符串拆分
- [字符串拆分](String-split.md)
