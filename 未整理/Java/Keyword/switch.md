# 关键字 switch

#### 当进行case判断时，JVM会自动从上到下扫描，寻找匹配的case：
- 未找到-执行默认的case
- 当每个case都不存在break时，JVM并不会顺序输出每个case对应的返回值，而是继续匹配，匹配不成功，则返回默认case。
- 当每个case都不存在break时，匹配成功后，从当前case开始，依次返回后续所有case的返回值。
- 若当前匹配成功的case不存在break，则从当前case开始，依次返回后续case的返回值，直到遇到break，跳出判断。

```text
// swithc-case 格式
// 变量类型：int/short/char/byte/enum
switch(变量){
    case 变量值1：
        // ;
        break;
    case 变量值2:
        // ;
        break;
        ......
   case default:
        // ;
        break;
}
```

当输入type=4时，以下代码输出？
```
switch (type) {
    default:
        System.out.println(4);
    case 1:
        System.out.println(1);
    case 2:
        System.out.println(2);
    case 3:
        System.out.println(3);
}

// 结果：
4
1
2
3
// 原因：当进行case判断时，JVM会自动从上到下扫描，寻找匹配的case
// 未找到-执行默认的case，如果每个case都不存在break时，从当前case开始，依次返回后续所有case的返回值。 
```