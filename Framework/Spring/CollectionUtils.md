## CollectionUtils 工具类

> CollectionUtils可以使代码更加简洁和安全。 

### 目录
- 集合判断
    - [集合是否为空](#集合是否为空)
    - [集合是否不为空](#集合是否不为空)
    - [集合是否相等](#集合是否相等)
- [并集](#并集)
- [交集](#交集)
- [交集的补集（析取）](#交集的补集（析取）)
- [差集（扣除）](#差集（扣除）)
- [不可修改的集合](#不可修改的集合)


### 集合是否为空

    CollectionUtils.isEmpty(null); // true
    CollectionUtils.isEmpty(new ArrayList()); // true　　
    CollectionUtils.isEmpty({a,b}); // false

### 集合是否不为空

    CollectionUtils.isNotEmpty(null); // false
    CollectionUtils.isNotEmpty(new ArrayList()); // false
    CollectionUtils.isNotEmpty({a,b}); // true

### 集合是否相等

    CollectionUtils.isEqualCollection(listA, listB)

### 并集

    CollectionUtils.union(listA, listB)

### 交集

    CollectionUtils.intersection(listA, listB)

### 交集的补集（析取）

    CollectionUtils.disjunction(listA, listB)

### 差集（扣除）

    CollectionUtils.subtract(listA, listB)

### 不可修改的集合

    CollectionUtils.unmodifiableCollection(c)
    
Collections.unmodifiableCollection可以得到一个集合的镜像，它的返回结果是不可直接被改变，否则会提示错误

java.lang.UnsupportedOperationException
at org.apache.commons.collections.collection.UnmodifiableCollection.add(UnmodifiableCollection.java:75)
