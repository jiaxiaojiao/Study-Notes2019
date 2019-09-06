## JDK8特性

> jdk1.8的一些新特性主要还是简化了代码的写法，减少了部分开发量。

### 目录
- [红黑树](#红黑树)
- [Stream 流处理](#Stream-流处理)
- [Lambda表达式](#Lambda表达式)
- [接口的默认方法与静态方法](#接口的默认方法与静态方法)
- [函数式接口](#函数式接口)
- [方法与构造函数的引用](#方法与构造函数的引用)
- [Date Time API](#Date-Time-API)
- [Optional](#Optional)

### 红黑树

对HashMap等Map集合的数据结构优化。

### Stream 流处理

- toList  把流中所有元素收集到List中
- toSet  把流中的所有元素收集到Set中，删除重复项
- toCollection  把流中所有元素收集到给定的供应源创建的集合中
- Counting  计算流中元素个数
- SummingInt  对流中元素的一个整数属性求和
- averagingInt  计算流中元素Integer属性的平均值
- Joining  连续流中每个元素的toString方法生成的字符串
- maxBy  一个包裹了流中按照给定比较器选出的最大元素的optional，如果为空返回的是Optional.empty()
- minBy  一个包裹了流中按照给定比较器选出的最小元素的optional，如果为空返回的是Optional.empty()
- Reducing  从一个作为累加器的初始值开始利用binaryOperator与流中的元素逐个结合，从而将流归约为单个值
- collectingAndThen  包裹另一个转换器，对其结果应用转换函数
- groupingBy  根据流中元素的某个值对流中的元素进行分组，并将属性值作为结果map的键。
- partitioningBy  根据流中每个元素应用谓语的结果来对项目进行分区

### Lambda表达式
- Lambda 表达式处理List

### 接口的默认方法与静态方法

### 函数式接口

“函数式接口”是指仅仅只包含一个抽象方法的接口，每一个该类型的lambda表达式都会被匹配到这个抽象方法。

jdk1.8提供了一个@FunctionalInterface注解来定义函数式接口。

函数式接口可以对现有的函数友好地支持 lambda。

JDK 1.8 之前已有的函数式接口:
- java.lang.Runnable
- java.util.concurrent.Callable
- java.security.PrivilegedAction
- java.util.Comparator
- java.io.FileFilter
- java.nio.file.PathMatcher
- java.lang.reflect.InvocationHandler
- java.beans.PropertyChangeListener
- java.awt.event.ActionListener
- javax.swing.event.ChangeListener

JDK 1.8 新增加的函数接口：
- java.util.function

### 方法与构造函数的引用

### Date Time API

加强了对时间和日期的处理。

Java 8 在 java.time 包下提供了很多新的 API。以下为两个比较重要的 API：
- Local(本地) − 简化了日期时间的处理。
- Zoned(时区) − 通过制定的时区处理日期时间。

常用的类：
- LocalDate为日期处理类
- LocalTime为时间处理类
- LocalDateTime为日期时间处理类

### Optional 