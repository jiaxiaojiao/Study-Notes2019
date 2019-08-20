# 计算

## 题目一
```
    // 计算 f(8)的值，并用程序实现。 // 结果： countTest(8) 21
	//	F(1)=1 
	//	F(2)=1 
	//	F(3)=2 
	//	F(4)=3 
	//	F(5)=5 
	//	F(6)=8 
	//	F(7)=13
	//	F(8)=? 
	public static int countTest(int n){
		int result = 0;
		if(n == 1){
			result = 1;
		}
		
		if(n == 2){
			result = 1;
		}
		
		if(n > 2){
			result = countTest(n-1)+countTest(n-2);
		}
		return result;
	}
```

## 题目二

```
++i 与 i++ 的区别

i++ 在程序执行完毕后进行自增
++i 在程序开始前进行自增
```
