# TreeSet

TreeSet实现了SortedSet接口，它是一个有序的集合类，TreeSet的底层是通过TreeMap实现的。TreeSet并不是根据插入的顺序来排序，而是根据实际的值的大小来排序。TreeSet也支持两种排序方式：
- 自然排序
- 自定义排序

TreeSet的重要特性：
- TreeSet实现SortedSet接口，因此不允许重复值。
- TreeSet中的对象按排序和升序存储。
- TreeSet不保留元素的插入顺序，但元素按键排序。
- TreeSet不允许插入异类对象。如果尝试添加hetrogeneous对象，它将在运行时抛出classCastException。
- TreeSet是存储大量已排序信息的绝佳选择，因为它可以更快地访问和检索，因此可以快速访问这些信息。
- TreeSet基本上是像Red-Black Tree这样的自平衡二叉搜索树的实现。因此，添加，删除和搜索等操作需要O（Log n）时间。并且按排序顺序打印n个元素的操作需要O（n）时间。


#### 继承关系
```text
java.lang.Object 
    java.util.AbstractCollection<E> 
        java.util.AbstractSet<E> 
            java.util.TreeSet<E> 
```

#### 实现接口
````text
Serializable, Cloneable, Iterable<E>, Collection<E>, NavigableSet<E>, Set<E>, SortedSet<E>
````

#### 基本属性
```text
private transient NavigableMap<E,Object> m;  //存放元素的集合
private static final Object PRESENT = new Object();  //m中key 对应的value 
```

#### 构造方法
```text
//相同包下可以访问的构造方法，将指定的m赋值为m 
TreeSet(NavigableMap<E,Object> m) {
    this.m = m;
}
//无参构造方法，创建一个空的TreeMap对象，并调用上面的构造方法
public TreeSet() {
    this(new TreeMap<E,Object>());
}
//指定比较器，并用指定的比较器创建TreeMap对象
public TreeSet(Comparator<? super E> comparator) {
    this(new TreeMap<>(comparator));
}
//将指定的集合C转化为TreeSet
public TreeSet(Collection<? extends E> c) {
    this();
    addAll(c);
}
//将SortedMap中的元素转化为TreeMap对象
public TreeSet(SortedSet<E> s) {
    this(s.comparator());
    addAll(s);
}
```

通过上面的构造方法，可以看出TreeSet的底层是用TreeMap实现的。在构造方法中会创建一个TreeMap实例，用于存放元素，另外TreeSet是有序的，也提供了制定比较器的构造函数，如果没有提供比较器，则采用key的自然顺序进行比较大小，如果指定的比较器，则采用指定的比较器，进行key值大小的比较。

#### 同步TreeSet
TreeSet中的实现在某种意义上不同步，即如果多个线程同时访问树集，并且至少有一个线程修改了该集，则必须在外部进行同步。这通常通过在自然封装集合的某个对象上进行同步来实现。如果不存在此类对象，则应使用Collections.synchronizedSortedSet方法“包装”该集合。这最好在创建时完成，以防止对集合的意外不同步访问：

```text
TreeSet ts = new TreeSet();
Set syncSet = Collections.synchronziedSet(ts);
```

#### TreeSet类的方法
TreeSet实现SortedSet，因此它具有Collection，Set和SortedSet接口中所有方法的可用性。以下是Treeset接口中的方法。

- void add（Object o）：此方法将根据TreeSet中的某些排序顺序添加指定的元素。不会添加重复的entires。
- boolean addAll（Collection c）：此方法将指定Collection的所有元素添加到集合中。Collection中的元素应该是同类的，否则将抛出ClassCastException。Collection的重复条目不会添加到TreeSet中。
- void clear（）：此方法将删除所有元素。
- boolean contains（Object o）：如果TreeSet中存在给定元素，则此方法将返回true，否则返回false。
- Object first（）：如果TreeSet不为null，则此方法将返回TreeSet中的第一个元素，否则将抛出NoSuchElementException。
- Object last（）：如果TreeSet不为null，则此方法将返回TreeSet中的最后一个元素，否则将抛出NoSuchElementException。
- SortedSet headSet（Object toElement）：此方法将返回TreeSet的元素，这些元素小于指定的元素。
- SortedSet tailSet（Object fromElement）：此方法将返回TreeSet的元素，这些元素大于或等于指定的元素。
- SortedSet subSet（Object fromElement，Object toElement）：此方法将返回从fromElement到toElement的元素。fromElement是包含的，toElement是独占的。
- boolean isEmpty（）：如果此set不包含任何元素，则此方法用于返回true;对于相反的情况，此方法用于返回false。
- Object clone（）：该方法用于返回集合的浅表副本，这只是一个简单的复制集合。
- int size（）：此方法用于返回集合的大小或集合中存在的元素数量。
- boolean remove（Object o）：此方法用于从集合中返回特定元素。
- Iterator iterator（）：返回一个迭代器，用于迭代集合的元素。
- Comparator comparator（）：此方法将返回用于对TreeSet中的元素进行排序的Comparator，如果使用默认的自然排序顺序，它将返回null。

#### 源码解析

```text
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable {

    //存放元素的map对象
    private transient NavigableMap<E,Object> m;

    //key-value ,不同的键都会对象相同的value, value = PRESENT
    private static final Object PRESENT = new Object();

    //指定的map对象
    TreeSet(NavigableMap<E,Object> m) {
        this.m = m;
    }

    //无参构造方法，初始化一个TreeMap对象
    public TreeSet() {
        this(new TreeMap<E,Object>());
    }

    //构造方法，指定比较器
    public TreeSet(Comparator<? super E> comparator) {
        this(new TreeMap<>(comparator));
    }

    //将集合中的元素转化为TreeSet存储
    public TreeSet(Collection<? extends E> c) {
        this();
        addAll(c);
    }

    //构造方法，SortedSet转化为TreeSet存储，并使用SortedSet的比较器
    public TreeSet(SortedSet<E> s) {
        this(s.comparator());
        addAll(s);
    }

    //遍历方法，返回m.keyset集合
    public Iterator<E> iterator() {
        return m.navigableKeySet().iterator();
    }

    //逆序排序的迭代器
    public Iterator<E> descendingIterator() {
        return m.descendingKeySet().iterator();
    }

    /**
     * @since 1.6
     */
    public NavigableSet<E> descendingSet() {
        return new TreeSet<>(m.descendingMap());
    }

    //返回 m 包含的键值对的数量
    public int size() {
        return m.size();
    }

    //是否为空
    public boolean isEmpty() {
        return m.isEmpty();
    }

    //是否包含指定的key
    public boolean contains(Object o) {
        return m.containsKey(o);
    }

    //添加元素，调用m.put方法实现
    public boolean add(E e) {
        return m.put(e, PRESENT)==null;
    }

    //删除方法，调用m.remove()方法实现
    public boolean remove(Object o) {
        return m.remove(o)==PRESENT;
    }

    //清除集合
    public void clear() {
        m.clear();
    }

    //将一个集合中的所有元素添加到TreeSet中
    public  boolean addAll(Collection<? extends E> c) {
        // Use linear-time version if applicable
        if (m.size()==0 && c.size() > 0 &&
            c instanceof SortedSet &&
            m instanceof TreeMap) {
            SortedSet<? extends E> set = (SortedSet<? extends E>) c;
            TreeMap<E,Object> map = (TreeMap<E, Object>) m;
            Comparator<? super E> cc = (Comparator<? super E>) set.comparator();
            Comparator<? super E> mc = map.comparator();
            if (cc==mc || (cc != null && cc.equals(mc))) {
                map.addAllForTreeSet(set, PRESENT);
                return true;
            }
        }
        return super.addAll(c);
    }

    //返回子集合，通过 m.subMap()方法实现
    public NavigableSet<E> subSet(E fromElement, boolean fromInclusive,
                                  E toElement,   boolean toInclusive) {
        return new TreeSet<>(m.subMap(fromElement, fromInclusive,
                                       toElement,   toInclusive));
    }

    //返回set的头部
    public NavigableSet<E> headSet(E toElement, boolean inclusive) {
        return new TreeSet<>(m.headMap(toElement, inclusive));
    }

    //返回尾部
    public NavigableSet<E> tailSet(E fromElement, boolean inclusive) {
        return new TreeSet<>(m.tailMap(fromElement, inclusive));
    }

    //返回子Set
    public SortedSet<E> subSet(E fromElement, E toElement) {
        return subSet(fromElement, true, toElement, false);
    }

    //返回set的头部
    public SortedSet<E> headSet(E toElement) {
        return headSet(toElement, false);
    }

    //返回set的尾部
    public SortedSet<E> tailSet(E fromElement) {
        return tailSet(fromElement, true);
    }
    //返回m使用的比较器
    public Comparator<? super E> comparator() {
        return m.comparator();
    }

    //返回第一个元素
    public E first() {
        return m.firstKey();
    }
    //返回最后一个元素
    public E last() {
        return m.lastKey();
    }

    //返回set中小于e的最大的元素
    public E lower(E e) {
        return m.lowerKey(e);
    }

    //返回set中小于/等于e的最大元素
    public E floor(E e) {
        return m.floorKey(e);
    }

    //返回set中大于/等于e的最大元素
    public E ceiling(E e) {
        return m.ceilingKey(e);
    }

    //返回set中大于e的最小元素
    public E higher(E e) {
        return m.higherKey(e);
    }

    //获取TreeSet中第一个元素，并从Set中删除该元素
    public E pollFirst() {
        Map.Entry<E,?> e = m.pollFirstEntry();
        return (e == null) ? null : e.getKey();
    }

    //获取TreeSet中最后一个元素，并从Set中删除该元素
    public E pollLast() {
        Map.Entry<E,?> e = m.pollLastEntry();
        return (e == null) ? null : e.getKey();
    }

    //克隆方法
    public Object clone() {
        TreeSet<E> clone = null;
        try {
            clone = (TreeSet<E>) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new InternalError();
        }

        clone.m = new TreeMap<>(m);
        return clone;
    }

    //将对象写入到输出流中。
    private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException {
        // Write out any hidden stuff
        s.defaultWriteObject();

        // Write out Comparator
        s.writeObject(m.comparator());

        // Write out size
        s.writeInt(m.size());

        // Write out all elements in the proper order.
        for (E e : m.keySet())
            s.writeObject(e);
    }

    //从输入流中读取对象的信息
    private void readObject(java.io.ObjectInputStream s)
        throws java.io.IOException, ClassNotFoundException {
        // Read in any hidden stuff
        s.defaultReadObject();

        // Read in Comparator
        Comparator<? super E> c = (Comparator<? super E>) s.readObject();

        // Create backing TreeMap
        TreeMap<E,Object> tm;
        if (c==null)
            tm = new TreeMap<>();
        else
            tm = new TreeMap<>(c);
        m = tm;

        // Read in size
        int size = s.readInt();

        tm.readTreeSet(size, s, PRESENT);
    }
    //序列化版本号
    private static final long serialVersionUID = -2479143000061671589L;
}
```

## 总结

TreeSet是一个有序的集合，基于TreeMap实现，支持两种排序方式：自然排序和定制排序。

TreeSet是非同步的，线程不安全的。