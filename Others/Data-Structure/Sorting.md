# 排序

排序 Sorting : 将一组数据，按特定的规则调换位置，使数据具有某种顺序关系（递增或递减）。

## 排序的分类

排序可以按照执行时所使用的内存分为两种方式：

1. 内部排序。 排序的数据量小，可以完全在内存内进行排序。

2. 外部排序。 排序的数据量无法直接在内存内进行排序，必须使用辅助存储器。

#### 排序算法分析

**算法是否稳定：**

- 稳定的排序（Stable Sort）是数据在经过排序后，两个相同键值的记录仍然保持原来的次序。

**时间复杂度（Time complexity）：**

- 最好情况 Best Case

- 最坏情况 Worst Case

- 平均情况 Average Case

**空间复杂度（Space complexity）:**

空间复杂度： 算法在执行过程中所需付出的额外内存空间。

#### 常见的内部排序法

**简单排序法：** 

- [冒泡排序（Bubble Sort）](Sorting-Algorithm/Bubble-Sort.md) 

    - 稳定排序法
    - 空间复杂度为最佳，只需一个额外空间 O(1) 

- [选择排序法 Selection Sort](Sorting-Algorithm/Selection-Sort.md) 

    - 不稳定排序法
    - 空间复杂度为最佳，只需一个额外空间 O(1) 
    
- [插入排序法 Insertion Sort](Sorting-Algorithm/Insertion-Sort.md)

    - 稳定排序法
    - 空间复杂度为最佳，只需一个额外空间 O(1) 

- [希尔排序法 Shell Sort](Sorting-Algorithm/Shell-Sort.md) 

    - 稳定排序法
    - 空间复杂度为最佳，只需一个额外空间 O(1) 

- [合并排序法 Merge Sort](Sorting-Algorithm/Merge-Sort.md)

**高级排序法：**

- [快速排序法 Quick Sort](Sorting-Algorithm/Quick-Sort.md)

    - 不稳定排序法
    - 空间复杂度最差为 O(n)，最佳为 O(log<sub>2</sub>n)

- [堆积排序法 Heap Sort](Sorting-Algorithm/Heap-Sort.md) 

    - 不稳定排序法
    - 空间复杂度为最佳，只需一个额外空间 O(1) 

- [基数排序法 Radix Sort](Sorting-Algorithm/Radix-Sort.md) 

    - 稳定排序法
    - 空间复杂度为 O(np) ， n为原始数据的个数，p为基底。

#### 常见的外部排序法

- 直接合并排序法

- k路合并法

- 多相合并法