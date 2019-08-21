# JDK 1.8 更新 - 接口的默认方法与静态方法

## 接口的默认方法与静态方法。

> 接口中可以定义默认实现方法和静态方法。

在接口中可以使用default和static关键字来修饰接口中定义的普通方法
```text
public interface Interface {
    default  String getName(){
        return "zhangsan";
    }
 
    static String getName2(){
        return "zhangsan";
    }
}
```
default方法是所有的实现类都不需要去实现的就可以直接调用。
