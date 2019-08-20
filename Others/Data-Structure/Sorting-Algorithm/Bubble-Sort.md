# 冒泡排序

又称交换排序法。

冒泡排序法的比较方式由第一个元素开始，比较相邻元素大小，若大小顺序有误，则对调后再进行下一个元素的比较。如此扫描过一次之后就可以确保最后一个元素是位于正确的顺序。接着再逐步进行第二次扫描，直到完成所有元素的排序关系为止。

```text
int arr[] = {6,5,9,7,2,8};
int i,j,temp;
for (i=arr.length-1; i>0; i--){ // 扫描次数
    for (j=0; j<i; j++){ // 比较交换次数
        // 比较 交换
        if(arr[j]>arr[j+1]){
            temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }
    }
    System.out.println(Arrays.toString(arr));
}

// 改良版：添加判断 提前中断排序，提高程序执行效率
int arr[] = {6,5,9,7,2,8};
int i,j,temp,flag;
for (i=arr.length-1; i>0; i--){ // 扫描次数
    flag = 0;
    for (j=0; j<i; j++){ // 比较交换次数
        // 比较 交换
        if(arr[j]>arr[j+1]){
            temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
            flag++;
        }
    }
    if (flag==0) break;
    System.out.println(Arrays.toString(arr));
}

```

## 冒泡法分析

1. 稳定排序法： 相邻两个比较后对调，不会更改原本排序。
2. 空间复杂度最佳： 只需要一个额外空间。
3. 最坏情况和平均情况都需要比较 n(n-1)/2 次，时间复杂度O(n<sup>2</sup>) 。
最好情况只需完成一次扫描，发现没有做交换的操作则表示已经排序完成，时间复杂度 O(n) 。
4. 适用于数量小或有部分数据已经排序的情况。