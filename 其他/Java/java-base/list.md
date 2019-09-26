# 集合类

## ArrayList
- [ArrayList 删除元素](list-array-remove.md)

### List 数组转换

#### List转换为Array

```text
ArrayList<String> list=new ArrayList<String>();
String[] strings = new String[list.size()];
list.toArray(strings);
```

#### 数组转换List

```text
String[] s = {"a","b","c"};
List list = java.util.Arrays.asList(s);
```

### 打乱顺序/随机排序

```text
Collections.shuffle(list);
```