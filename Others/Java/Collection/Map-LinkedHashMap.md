# LinedHashMap

## 描述

LinkedHashMap 继承自 HashMap，在 HashMap 基础上，通过维护一条双向链表，解决了 HashMap 不能随时保持遍历顺序和插入顺序一致的问题。

除此之外，LinkedHashMap 对访问顺序也提供了相关支持。在一些场景下，该特性很有用，比如缓存。在实现上，LinkedHashMap 很多方法直接继承自 HashMap，仅为维护双向链表覆写了部分方法。


## 基本用法

LinkedHashMap是HashMap的子类，但是内部还有一个双向链表维护键值对的顺序，每个键值对既位于哈希表中，也位于双向链表中。LinkedHashMap支持两种顺序插入顺序 、 访问顺序

- 插入顺序：先添加的在前面，后添加的在后面。修改操作不影响顺序。

- 访问顺序：所谓访问指的是get/put操作，对一个键执行get/put操作后，其对应的键值对会移动到链表末尾，所以最末尾的是最近访问的，最开始的是最久没有被访问的，这就是访问顺序。

#### 指定按照访问顺序排序

LinkedHashMap有5个构造方法，其中4个都是按插入顺序，只有一个是可以指定按访问顺序：

```text
public LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)
```

其中参数accessOrder就是用来指定是否按访问顺序，如果为true，就是访问顺序。


举例： 

默认情况下，LinkedHashMap是按照插入顺序的

```text
Map<String, Integer> seqMap = new LinkedHashMap<>();
seqMap.put("c",100);
seqMap.put("d",200);
seqMap.put("a",500);
seqMap.put("d",300);
for(Entry<String,Integer> entry:seqMap.entrySet()){
	System.out.println(entry.getKey()+" "+entry.getValue());
}


键是按照:“c”, “d”,"a"的顺序插入的，修改d不会修改顺序，输出为：
c 100
d 300
a 500

```

按访问顺序：

```text
Map<String, Integer> accessMap = new LinkedHashMap<>(16,0.75f,true);
accessMap.put("c",100);
accessMap.put("d",200);
accessMap.put("a",500);
accessMap.get("c");
accessMap.put("d",300);
for(Map.Entry<String,Integer> entry:accessMap.entrySet()){
    System.out.println(entry.getKey()+" "+entry.getValue());
}

输出为：
a 500
c 100
d 300

```

#### 按访问有序实现缓存

```text
import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCache<K, V> extends LinkedHashMap<K, V> {

    private int maxEntries;

    public LRUCache(int maxEntries) {
        super(16, 0.75f, true);
        this.maxEntries = maxEntries;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > maxEntries;
    }

}

在LinkedHashMap添加元素后，会调用removeEldestEntry防范，传递的参数时最久没有被访问的键值对，如果方法返回true，这个最久的键值对就会被删除。LinkedHashMap中的实现总返回false，该子类重写后即可实现对容量的控制。

使用该缓存：

        LRUCache<String,Object> cache = new LRUCache<>(3);
        cache.put("a","abstract");
        cache.put("b","basic");
        cache.put("c","call");
        cache.get("a");
        cache.put("d","滴滴滴");
        System.out.println(cache); // 输出为：{c=call, a=abstract, d=滴滴滴}


```