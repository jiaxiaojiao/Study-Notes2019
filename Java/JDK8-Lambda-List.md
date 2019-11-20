## Lambda 表达式处理List
1. 从List中获取一个属性的集合

    1111

2. List<A>转成List<B>

    2222
3. 遍历List
4. List转成Map
5. List分组
6. 过滤
7. 求和


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

