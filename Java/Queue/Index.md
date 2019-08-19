## Queue 队列

> 队列是一种特殊的线性表，它只允许在表的前端进行删除操作，在表的后端进行插入操作。

### 目录：

- [LinkedList](../Collections/LinkedList.md)

### 队列用法演示

LinkedList类实现了接口Deque<E> （接口Deque<E>继承队列Queue<E>），可以把LinkedList当成队列Queue来用：

```Java
package com.jocelyn.spark;

import java.util.LinkedList;
import java.util.Queue;

/**
 * @description: 测试
 * @author: v-jiaxiaojiao
 * @create: 2019/08/19 15:55
 */
public class Test {
    public static void main(String[] args) {
        // add() remove()方法在失败时会抛出异常（不推荐）
        Queue<String> queue = new LinkedList<String>();
        // 添加元素
        queue.offer("a");
        queue.offer("b");
        queue.offer("c");
        queue.offer("d");
        queue.offer("e");
        System.out.println("队列：");
        for (String q : queue) {
            System.out.print(q);
        }
        System.out.println();

        System.out.println("第一个元素，并且在队列中删除（poll）:" + queue.poll());
        System.out.println("队列：");
        for (String q : queue) {
            System.out.print(q);
        }
        System.out.println();

        System.out.println("第一个元素（element）当队列为空时，抛出异常NoSuchElementException:" + queue.element());
        System.out.println("队列：");
        for (String q : queue) {
            System.out.print(q);
        }
        System.out.println();

        System.out.println("第一个元素（peek）当队列为空时，返回null:" + queue.peek());
        System.out.println("队列：");
        for (String q : queue) {
            System.out.print(q);
        }
        System.out.println();
    }
}

```

执行结果：
```text
队列：
abcde
第一个元素，并且在队列中删除（poll）:a
队列：
bcde
第一个元素（element）当队列为空时，抛出异常NoSuchElementException:b
队列：
bcde
第一个元素（peek）当队列为空时，返回null:b
队列：
bcde
```

方法总结：
- 添加元素
    - offer(E e)  在LinkedList中offer(E e)仅仅调用了add(E e)方法，两者是一样的。
    - add(E e) 
- 移除队列的头部元素
    - remove()  当队列为空时，抛出异常NoSuchElementException。
    - poll()  当队列为空时，返回null
- 查询队列的头部元素
    - element()  当队列为空时，抛出异常NoSuchElementException。
    - peek()  当队列为空时，返回null
