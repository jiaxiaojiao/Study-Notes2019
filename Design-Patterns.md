## 设计模式

#### 单例模式

**线程安全的单例模式：**

- 用静态工厂方法实现单例
```Java
public class Singleton{
    //initailzed during class loading
    private static final Singleton INSTANCE = new Singleton();

    //to prevent creating another instance of Singleton
    private Singleton(){}

    public static Singleton getSingleton(){
        return INSTANCE;
    }
}
```
- 用双检索实现单例

```Java
public class DoubleCheckedLockingSingleton{
    
    private volatile DoubleCheckedLockingSingleton INSTANCE;
    
    private DoubleCheckedLockingSingleton(){}
    
    public DoubleCheckedLockingSingleton getInstance(){
        if(INSTANCE == null){
            synchronized(DoubleCheckedLockingSingleton.class){
                //double checking Singleton instance
                if(INSTANCE == null){
                    INSTANCE = new DoubleCheckedLockingSingleton();
                }
            }
        }
        return INSTANCE;
    }
}

```

- 用枚举实现单例模式

```Java
public enum EasySingleton{
    INSTANCE;
}
```

#### 代理模式

- 静态代理

- 动态代理

#### 观察者模式

观察者（Observer）模式的定义：指多个对象间存在一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。这种模式有时又称作发布-订阅模式、模型-视图模式，它是对象行为型模式。

观察者模式是一种对象行为型模式，其主要优点如下：
- 降低了目标与观察者之间的耦合关系，两者之间是抽象耦合关系。
- 目标与观察者之间建立了一套触发机制。

它的主要缺点如下：
- 目标与观察者之间的依赖关系并没有完全解除，而且有可能出现循环引用。
- 当观察者对象很多时，通知的发布会花费很多时间，影响程序的效率。
