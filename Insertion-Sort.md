# 插入排序法

插入排序法： 将数组中的元素，逐一与已排序好的数据做比较，再讲该数组元素插入适当的位置。

```text
int arr[] = {6,5,9,7,2,8};
int i,j,temp;
for (i=1; i<arr.length; i++){ // 扫描次数
    temp = arr[i];
    j = i - 1;
    while (j>=0 && temp<arr[j]){
        arr[j + 1] = arr[j];
        j--;
    }
    arr[j + 1] = temp;
    System.out.println(Arrays.toString(arr));
}

```

## 插入排序法分析

1. 稳定排序法

2. 空间复杂度最佳： 只需一个额外空间。

3. 最坏情况 和 平均情况需比较 n(n-1)/2 , 时间复杂度 O(n<sup>2</sup>) 。 
   最好情况时间复杂度 O(n)

4. 适用于大部分数据已经排序或已排序数据库新增数据库进行排序的情况。

5. 会造成数据的大量搬移，建议在链表上使用。   