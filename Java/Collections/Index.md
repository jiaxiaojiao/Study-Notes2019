## Java 集合框架

### 目录
- List
    - ArrayList
    - [LinkedList](LinkedList.md)
- Set
    - HashSet
- Map
    - HashMap
    - [Map的keySet()顺序问题](#顺序问题-keySet)
    
### 顺序问题 keySet

LinkedHashMap.keySet()拿到的Set是按照顺序的。

Hashtable、TreeMap、HashMap keySet()拿到的Set都是乱序的。

