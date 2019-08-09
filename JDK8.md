## JDK8特性

#### Stream 流处理

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

#### Lambda表达式

```text
// 从List中获取一个属性集合：
List<Long> ids = userList.stream().map(user -> user.getId()).collect(Collectors.toList());

List<A> 转成 List<B>：
// List<A> aList = ...;
List<B> bList = aList.stream().map(a ->{
// 在此转把A转换为B
    return new B();
}).collect(Collectors.toList());

List<User> list ...;
// 遍历
list.stream().forEach(user -> {});
// List转为Map
Map<Long, User> map = list.stream().collect(Collectors.toMap(User::getId, a -> a,(k1, k2) -> k1));
Map<Long, User> map = list.stream().collect(Collectors.toMap(User::getId,user -> user));
// List分组
Map<String, List<User>> map = list.stream().collect(Collectors.groupingBy(User::getName));
// 过滤
List<User> filterList = list.stream().filter(user -> user.getName().equals("XX")).collect(Collectors.toList());
// 求和
int sumAge = list.stream().mapToInt(User::getAge).sum();
```

