# 工具 Collections

## 用法
```text
    //排序，直接调用sort方法排序，排序方式是自燃排序，即升序排序
    Collections.sort(lists);
    
    // 通过实现Comparator接口的compare方法来完成自定义排序：倒序排序等
    Collections.sort(lists,new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            // 返回值为int类型，大于0表示正序，小于0表示逆序
            return o2-o1;
        }
    });
```
### 用法总结
1. 对于String或Integer这些已经实现Comparable接口的类来说，可以直接使用Collections.sort方法传入list参数来实现默认方式（正序）排序；
2. 如果不想使用默认方式（正序）排序，可以通过Collections.sort传入第二个参数类型为Comparator来自定义排序规则；
3. 对于自定义类型，如果想使用Collections.sort的方式一进行排序，可以通过实现Comparable接口的compareTo方法来进行，如果不实现，则参考第2点；
4. jdk1.8的Comparator接口有很多新增方法，其中有个reversed()方法比较实用，是用来切换正序和逆序的
