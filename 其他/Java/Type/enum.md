# 枚举


```
1. 枚举是1.5以后的新特性
2. enum 和 class、interface 的地位一样
3. 使用enum定义的枚举类默认继承了java.lang.Enum。
4. 枚举类的构造器只能是私有的

```

## 枚举的用法

```
// 1.  常量用法。
public enum ColorEnum {
    RED,BLUE,GREEN
}

// 2.  JDK1.6以后switch语句支持枚举，更代码可读性更强。
public enum Signal{
    RED,BLUE,GREEN
}
public class TrafficLight {
    Signal color = Signal.RED;
    
    public void change() {
        switch (color) {
            case RED:
            color = Signal.BLUE;
            break;
            case BLUE:
            color = Signal.GREEN;
            break;
            case GREEN:
            color=Signal.RED;
            break;
        }
    }
}

// 3. 增加自己的字段以及一些辅助方法
public enum ColorEnum {
    RED("red","红色"),GREEN("green","绿色"),BLUE("blue","蓝色");
    //防止字段值被修改，增加的字段也统一final表示常量
    private final String key;
    private final String value;
    
    private ColorEnum(String key,String value){
        this.key = key;
        this.value = value;
    }
    //根据key获取枚举
    public static ColorEnum getEnumByKey(String key){
        if(null == key){
            return null;
        }
        for(ColorEnum temp:ColorEnum.values()){
            if(temp.getKey().equals(key)){
                return temp;
            }
        }
        return null;
    }
    public String getKey() {
        return key;
    }
    public String getValue() {
        return value;
    }
}

// 4. 覆盖枚举的方法
public enum Color {
    RED("红色", 1), GREEN("绿色", 2), BLANK("白色", 3), YELLO("黄色", 4);
	// 成员变量
	private String name;
	private int index;
	// 构造方法
	private Color(String name, int index) {
		this.name = name;
		this.index = index;
	}
	//覆盖方法
	@Override 
	public String toString() {
		return this.index+"_"+this.name;
	}
}

// 5. 实现接口

```
## 枚举的好处
1. 枚举类更加直观，类型安全
2. 枚举型可以直接跟数据库打交道
3. switch语句支持枚举，使代码的可读性更强。

## 枚举的常用方法
1. values()获取存储枚举中所有常量实例的数组。常配合foreach完成遍历

```
 for(ColorEnum temp:ColorEnum.values()){
            System.out.println(temp);
    }
```

2. 构造方法，枚举的构造方法只能用private修饰符修饰
3. valueOf()通过常量名获取对应的枚举实例

```
ColorEnum red = ColorEnum.valueOf("RED");
　　System.out.println(red);
```

https://blog.csdn.net/qq_27093465/article/details/52180865
https://www.cnblogs.com/hyl8218/p/5088287.html
https://www.cnblogs.com/sister/p/4700702.html