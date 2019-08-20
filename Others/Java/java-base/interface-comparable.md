# 接口-Comparable
## 描述
    此接口强行对实现它的每个类的对象进行整体排序。
    这种排序被称为类的自然排序，类的 compareTo 方法被称为它的自然比较方法。
    实现此接口的对象列表（和数组）可以通过 Collections.sort（和 Arrays.sort）进行自动排序。
    实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。
    
    对于类 C(Collections) 的每一个 e1 (Element)和 e2 来说，
    当且仅当 e1.compareTo(e2) == 0 与 e1.equals(e2) 具有相同的 boolean 值时，类 C 的自然排序才叫做与 equals 一致。
    注意，null 不是任何类的实例，即使 e.equals(null) 返回 false，e.compareTo(null) 也将抛出 NullPointerException。

## 方法
    Comparable接口只提供了一个抽象方法：
    
    如果该对象小于、等于或大于指定对象，则分别返回负整数、零或正整数。
    根据不同类的实现返回不同，大部分返回1,0和-1三个数

返回值 | 方法 | 描述
---|---|---
int | compareTo(T o) | 比较此对象与指定对象的顺序。<br>o为要比较的对象
```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

## 要求
1. 实现类必须确保对于所有的 x 和 y 都存在 sgn(x.compareTo(y)) == -sgn(y.compareTo(x)) 的关系。（这意味着如果 y.compareTo(x) 抛出一个异常，则 x.compareTo(y) 也要抛出一个异常。）
2. 实现类还必须确保关系是可传递的：(x.compareTo(y)>0 && y.compareTo(z)>0) 意味着 x.compareTo(z)>0。
3. 最后，实现者必须确保 x.compareTo(y)==0 意味着对于所有的 z，都存在 sgn(x.compareTo(z)) == sgn(y.compareTo(z))。 强烈推荐 (x.compareTo(y)==0) == (x.equals(y)) 这种做法，但并不是 严格要求这样做。一般来说，任何实现 Comparable 接口和违背此条件的类都应该清楚地指出这一事实。推荐如此阐述：“注意：此类具有与 equals 不一致的自然排序。”

在前面的描述中，符号 sgn(expression) 指定 signum 数学函数，该函数根据 expression 的值是负数、零还是正数，分别返回 -1、0 或 1 中的一个值。


## 排序的两种方式
### 1. 实现接口Comparable
```java
// 实体类
public class T implements Comparable<T>{

    private String date;
    private int value;

    public T(String date, int value) {
        this.date = date;
        this.value = value;
    }
    
    @Override
    public int compareTo(T o) {
        return this.date.compareTo(o.date); // 升序
    }
    // getter setter
}
```
### 2. 重写Comparator方法
```java
public class Test{
    public static void testM(){
        TreeSet<T> ts = new TreeSet<T>(new Comparator<T>() {
            @Override
            public int compare(T o1, T o2) {
                return o2.getDate().compareTo(o1.getDate());// 降序
            }
        }); 
    }
}
```