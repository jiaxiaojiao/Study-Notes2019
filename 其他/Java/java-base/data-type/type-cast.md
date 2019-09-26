# 类型转换

## Integer > String
方法一:Integer类的静态方法toString()
```text
Integer a = 2;
String str = Integer.toString(a)
```
方法二:Integer类的成员方法toString()
```text
Integer a = 2;
String str = a.toString();
```
方法三:String类的静态方法valueOf()
```text
Integer a = 2;
String str = String.valueOf(a);
```

## Integer < String
当我们要把String转化为Integer时，一定要对String进行非空判断，否则很可能报空指针异常。
```text
String str = "123";
Integer i = null;
if(str!=null){
     i = Integer.valueOf(str);
}
```
## Date > String
```text
Date date = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
sdf.format(date)

sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
sdf.format(date);
sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
sdf.format(date);

```

## Date < String
在字符串转日期操作时，需要注意给定的模式必须和给定的字符串格式匹配，否则会抛出java.text.ParseException异常。
```text
String string = "2016-10-24 21:59:06";
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
sdf.parse(string);
```

## Double > Long
```text
double d = 88.88;  
long l = Math.round(d); 

Double obj = new Double("543267.90");
long l = obj.longValue();

```
## Double < Long
```text
long ll = 100L;  
double dd = (double) ll;

```


## List > Map