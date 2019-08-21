# 异常
以下代码最后会抛出一个异常，是第几行抛出的
```
try{
  throw new Exception("1");
}catch (IOException e){
  throw new Exception("2");
}catch (Exception e) {
  throw new Exception("3");
}finally {
  throw new Exception("4");
}
// 答案： finally里的Exception 4
```
