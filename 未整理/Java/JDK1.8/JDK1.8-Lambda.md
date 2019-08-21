# Lambda 表达式

> 闭包。

> Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。

> Lambda 表达式简化了代码。

```text
格式：  (parameters参数) -> expression表达式或方法体
```

> 为引入Lambda表达式，Java8新增了java.util.funcion包，里面包含常用的函数接口，这是Lambda表达式的基础，Java集合框架也新增部分接口，以便与Lambda表达式对接。lambda表达式本质上是一段匿名内部类，也可以是一段可以传递的代码

## Lambda 表达式简单例子
```text
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```

## 例子
需求：假设有一个字符串列表，需要打印出其中所有长度大于3的字符串.
- 原 增强的for循环
```text
ArrayList<String> list = new ArrayList<>(Arrays.asList("I", "love", "you", "too"));
for(String str : list){
    if(str.length()>3)
        System.out.println(str);
}
```
- 新 forEach() + 匿名内部类
```text
// 使用forEach()结合匿名内部类迭代
ArrayList<String> list = new ArrayList<>(Arrays.asList("I", "love", "you", "too"));
list.forEach(new Consumer<String>(){
    @Override
    public void accept(String str){
        if(str.length()>3)
            System.out.println(str);
    }
});
```
- 新 forEach() + Lambda表达式
```text
// 使用forEach()结合Lambda表达式迭代
ArrayList<String> list = new ArrayList<>(Arrays.asList("I", "love", "you", "too"));
list.forEach( str -> {
        if(str.length()>3)
            System.out.println(str);
    });
```

```text
Collections.sort(names, (a, b) -> b.compareTo(a));
```

总结：
1. Java8为容器新增一些有用的方法，这些方法有些是为完善原有功能，有些是为引入函数式编程，学习和使用这些方法有助于我们写出更加简洁有效的代码。
2. 函数接口虽然很多，但绝大多数时候我们根本不需要知道它们的名字，书写Lambda表达式时类型推断帮我们做了一切。
