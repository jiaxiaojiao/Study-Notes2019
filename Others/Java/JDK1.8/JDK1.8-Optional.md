# JDK 1.8 新特性 - Optional 类

> Optional 类是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。
  
> Optional 是个容器：它可以保存类型T的值，或者仅仅保存null。Optional提供很多有用的方法，这样我们就不用显式进行空值检测。
  
> Optional 类的引入很好的解决空指针异常。

## 类声明

以下是一个 java.util.Optional<T> 类的声明：
```text
public final class Optional<T>
extends Object
```