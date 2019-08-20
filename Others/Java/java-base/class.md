# 类


#### 内部类
``` java
// 内部类
// 创建静态内部类对象的一般形式为：  外部类类名.内部类类名 xxx = new 外部类类名.内部类类名()
// 创建成员内部类对象的一般形式为：  外部类类名.内部类类名 xxx = 外部类对象名.new 内部类类名()
public class Test{
    public static void main(String[] args){
           // 初始化Bean1
           //(1)
           Test test = new Test();
           Test.Bean1 bean1 = test.new Bean1();
           bean1.I++;
           // 初始化Bean2
           //(2)
           Test.Bean2 bean2 = new Test.Bean2();
           bean2.J++;
           //初始化Bean3
           //(3)
           Bean bean = new Bean();
           Bean.Bean3 bean3 = bean.new Bean3();
           bean3.k++;
    }
    class Bean1{
           public int I = 0;
    }
 
    static class Bean2{
           public int J = 0;
    }
}
 
class Bean{
    class Bean3{
           public int k = 0;
    }
}
```