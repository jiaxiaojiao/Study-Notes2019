## ArrayList 删除元素

### 错误一： for循环删除
```text
  for 循环 正序
  
  错误原因： ArrayList 有序集合，移除元素后数组元素移动下标改变，所以循环会漏掉数据。
  
  如何避免： 可以倒序删除。
  
  for(int i=list.size()-1;i>0; i--){
  }
```

### 错误二： for-each循环
```text
  for-each循环
  
  错误原因： 异常，并发修改异常： java.util.ConcurrentModificationException
  
  如何避免： 使用Iterator的remove
  Iterator<> it = list.iterator();
  while(it.hasNext()){
  }
```