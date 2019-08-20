# ArrayList


#### 1. ArrayList中的subList

关于集合类，《阿里巴巴Java开发手册》规定：

> 【强制】 ArrayList的subList结果不可强转成ArrayList，否则会抛出ClassCastException异常，即java.util.RandomAccessSubList cannot be cast to java.util.ArrayList.
说明： subList返回的是ArrayList的内部类SubList，并不是ArrayList，而是ArrayList的一个视图，对于SubList子列表的所有操作最终会反映在原列表上。

> 【强制】 在subList场景中，高度注意对原集合元素的增加或删除，均会导致子列表的遍历、增加、删除产生ConcurrentModificationException 异常。

subList是List接口中定义的一个方法，该方法主要用于返回一个集合中的一段、可以理解为截取一个集合中的部分元素，他的返回值也是一个List。

如果将返回值强转成ArrayList会报错。

原因： 

subList 方法返回的是一个视图。返回了一个类SubList，这个类是ArrayList的一个内部类。内部类SubList的构造函数SubList把原来的List和部分属性直接赋值给了自己。也就是说，SubList并没有重新创建一个List，而是直接引用了原有的List（返回了父类的视图），只是指定了范围（从fromIndex包括 到 toIndex不包括）。

SubList只是ArrayList的内部类，他们之间并没有继承关系，故无法直接进行强制类型转换。

**subList对List的影响/使用时的问题：**
- 通过set修改subList元素时，原List中对应的值也修改了。同样修改原List的值，subList也修改。
- 通过add添加subList元素时，原List也添加了元素。
- 通过add添加原List元素时，异常。

总结： 
- 对父(sourceList)子(subList)List做的非结构性修改（non-structural changes），都会影响到彼此。
- 对子List做结构性修改，操作同样会反映到父List上。
- 对父List做结构性修改，会抛出异常ConcurrentModificationException。

#### 2. 对比 ArrayList和linkedList Vector
1. 是否保证线程安全
    - ArrayList 方法是不同步的，也就是非线程安全。
    - LinkedList 方法是不同步的，也就是非线程安全。
    - Vector synchronize同步，是线程安全。性能较差。
2. 底层数据结构
    - Arraylist 底层使用的是 Object 数组。
    - LinkedList 底层使用的是 双向链表（JDK1.6之前为循环链表，JDK1.7取消了循环）
    - Vector 跟ArrayList一样，底层使用的是数组。
3. 插入和删除是否受元素位置的影响
    - ArrayList 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。 比如：执行add(E e) 方法的时候， ArrayList 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是O(1)。但是如果要在指定位置 i 插入和删除元素的话（add(int index, E element) ）时间复杂度就为 O(n-i)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。 
    - LinkedList 采用链表存储，所以插入，删除元素时间复杂度不受元素位置的影响，都是近似 O（1）而数组为近似 O（n）
    - Vector 跟ArrayList一样。
4. 是否支持快速随机访问（快速随机访问就是通过元素的序号快速获取元素对象(对应于get(int index) 方法)。）
    - ArrayList 支持快速随机访问
    - LinkedList 不支持高效的随机元素访问。
    - Vector 跟ArrayList一样。
5. 内存空间占用
    - ArrayList的空间浪费主要体现在在list列表的结尾会预留一定的容量空间。更多元素添加进来时会请求更大的空间，每次对size增长50%。
    - LinkedList的空间花费则体现在它的每一个元素都需要消耗比ArrayList更多的空间（因为要存放直接后继和直接前驱以及数据）。
    - Vector 更多元素添加进来时会请求更大的空间，每次请求其大小的双倍空间。




