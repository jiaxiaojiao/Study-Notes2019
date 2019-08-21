# 对字符串进行拆分 String.split()

## 1. 单参数拆分方法
```text
public String[] split(String regex)

```

- **参数**: regex-the delimiting regular expression,定界正则表达式

- **返回**: String[],字符串数组,它是根据给定正则表达式的匹配拆分此字符串确定的，如果表达式不匹配输入的任何部分，那么所得数组只具有一个元素，即此字符串。

- **抛出**： PatternSyntaxException - 如果正则表达式的语法无效

- **特点**: 该方法的作用就像是使用给定的表达式和限制参数 0 来调用两参数 split 方法,即是split(String regex,0)。因此，所得数组中不包括结尾空字符串。

### 拆分示例：
    拆分字符串"Harry James Potter",以空格进行拆分
    
```text
public class SplitDemo {
	public static void main(String[] args) {
		String nameStr="Harry James Potter";
		//"\\s"表示空格
		String[] nameStrArray=nameStr.split("\\s");
		//也可以来" "来进行拆分,这种方法要注意中间只能有一个空格，如果有两个空格则不能正常拆分，最后得到的仍是原有字符串
		//String[] nameStrArray=nameStr.split(" ");
		for(String name:nameStrArray){
			System.out.println(name);
		}
	}	
}

```

拆分结果
```text
Harry
James
Potter

```  

#### 拆分后的字符数组不包含节尾空字符串
用单参数split()方法拆分字符串时会发现有时拆分出来的字符串数组长度好像与预期不一致，这是因为当最后拆分出的那个字符串为空字符时，这个空字符不会加到数组中去。
示例:拆分"Harry#James#Potter###",以"#"号进行拆分，按感觉来说应该会拆分成六段

```text
import java.util.Arrays;
public class SplitDemo {
	public static void main(String[] args) {
		String nameStr="Harry#James#Potter###";
		String[] nameStrArray=nameStr.split("#");
		for(String name:nameStrArray){
			System.out.println(name);
		}
		System.out.println("数组长度为:"+nameStrArray.length);
		System.out.println("数组值为:"+Arrays.toString(nameStrArray));
	}	
}

```

运行结果如下：
```text
Harry
James
Potter
数组长度为:3
数组值为:[Harry, James, Potter]

```  

从结果来看，实际上拆分出的数组只有三位，##之间与之后的空字符串都不会被加入至这个数组中。

## 2. 双参数拆分方法
```text
public String[] split(String regex, int limit)

```

参数比上面方法多了一个int类型，limit 参数控制模式应用的次数，即拆分的次数,因此影响所得数组的长度。下面n所指为limit参数

- 如果该限制 n 大于 0，则模式将被最多应用 n - 1 次，数组的长度将不会大于 n，而且数组的最后一项将包含所有超出最后匹配的定界符的输入。

- 如果 n 为非正，那么模式将被应用尽可能多的次数，而且数组可以是任何长度。

- 如果 n 为 0，那么模式将被应用尽可能多的次数，数组可以是任何长度，并且结尾空字符串将被丢弃

### limit为正负数时的示例
依旧以"Harry#James#Potter###",以"#"号进行拆分
    
- 当limit为1时，拆分结果如下，数组长度应不大于1，即小于等于1
```text
String nameStr="Harry#James#Potter###";
String[] nameStrArray=nameStr.split("#",1);
//结果如下，字符串原样输出了，因为拆分只进行了1-1次,即0次
Harry#James#Potter###
数组长度为:1
数组值为:[Harry#James#Potter###]

``` 
- 当limit为4时，拆分了三次，数组长度应不大于4
```text
String[] nameStrArray=nameStr.split("#",4);
//拆分结果如下，最后一个字符串为"##",说明这两个还没被拆分
Harry
James
Potter
##
数组长度为:4
数组值为:[Harry, James, Potter, ##]

```

-  当limit为-1时,字符串会被尽可能地被多拆分
```text
String[] nameStrArray=nameStr.split("#",-1);
//拆分结果如下，数组长度为6，其中包含了三个空字符，说明将所有的#都进行了拆分，字符串不再有#存在
Harry
James
Potter



数组长度为:6
数组值为:[Harry, James, Potter, , , ]

```

-  当limit为-2时,拆分结果与-1时一致，所以当这个limit是负数时，不管传什么值，结果都是一致的。
```text
String[] nameStrArray=nameStr.split("#",-1);
//拆分结果与-1时一致
Harry
James
Potter



数组长度为:6
数组值为:[Harry, James, Potter, , , ]

```

## 3. 与str.split(regex,limit)结果相同的方法

以下运用字符串匹配的方法与字符串拆分方法返回的结果一致。

```text
Pattern.compile(regex).split(str, n)

```