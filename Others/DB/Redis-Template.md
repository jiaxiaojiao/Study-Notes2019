# Java 使用RedisTemplate

### 1. 注入 RedisTempplate

```text
@Autowired
private RedisTemplate<String,String> redisTemplate;

```

### 2. 保存和读取Set

```text
SetOperations<String, String> set = redisTemplate.opsForSet();
set.add("set1","22");  
set.add("set1","33");  
set.add("set1","44");  
Set<String> resultSet =redisTemplate.opsForSet().members("set1");  
System.out.println("resultSet:"+resultSet); 

运行结果为：
resultSet:[[set3, set2, set1]]  jedis

```

### 3. Hash结构，保存和读取map

```text
Map<String,String> map=new HashMap<String,String>();  
map.put("key1","value1");  
map.put("key2","value2");  
map.put("key3","value3");  
map.put("key4","value4");  
map.put("key5","value5");  
redisTemplate.opsForHash().putAll("map1",map);  
Map<String,String> resultMap= redisTemplate.opsForHash().entries("map1");  
List<String>reslutMapList=redisTemplate.opsForHash().values("map1");  
Set<String>resultMapSet=redisTemplate.opsForHash().keys("map1");  
String value=(String)redisTemplate.opsForHash().get("map1","key1");  
System.out.println("value:"+value);  
System.out.println("resultMapSet:"+resultMapSet);  
System.out.println("resultMap:"+resultMap);  
System.out.println("resulreslutMapListtMap:"+reslutMapList); 

运行结果为：
value:value1
resultMapSet:[key1, key2, key5, key3, key4]
resultMap:{key3=value3, key2=value2, key1=value1, key5=value5, key4=value4}
resulreslutMapListtMap:[value1, value2, value5, value3, value4]

```

### 4. 保存和读取list

```text
List<String> list1=new ArrayList<String>();
list1.add("a1");
list1.add("a2");
list1.add("a3");
 
List<String> list2=new ArrayList<String>();
list2.add("b1");
list2.add("b2");
list2.add("b3");
redisTemplate.opsForList().leftPush("listkey1",list1);
redisTemplate.opsForList().rightPush("listkey2",list2);
List<String> resultList1=(List<String>)redisTemplate.opsForList().leftPop("listkey1");
List<String> resultList2=(List<String>)redisTemplate.opsForList().rightPop("listkey2");
System.out.println("resultList1:"+resultList1);
System.out.println("resultList2:"+resultList2);
运行结果：
resultList1:[a1, a2, a3]
resultList2:[b1, b2, b3]

```

这里需要解释一下：不管是leftPush还是rightPush都可以用leftPop或者rightPoP任意一种获取到其中的值，不过就是获取的遍历方向不一样。有学过数据结构的人都知道里面循环链表是可以前后遍历的，就和这里的场景是一样的。如果还有不懂的话可以去看看这部分的源代码，其实就是遍历方向不同，所以效率也不同。所以最好leftPush用leftPoP遍历，rightPush用rightPoP遍历

### 5. 保存和读取String(最常用的)

```text
System.out.println("缓存正在设置。。。。。。。。。");
redisTemplate.opsForValue().set("key1","value1");
redisTemplate.opsForValue().set("key2","value2");
redisTemplate.opsForValue().set("key3","value3");
redisTemplate.opsForValue().set("key4","value4"); 
System.out.println("缓存已经设置完毕。。。。。。。");
String result1=redisTemplate.opsForValue().get("key1").toString();
String result2=redisTemplate.opsForValue().get("key2").toString();
String result3=redisTemplate.opsForValue().get("key3").toString();
System.out.println("缓存结果为：result："+result1+"  "+result2+"   "+result3);

```

### 6. 模糊匹配删除

```text
Set<String> keys = redisTemplate.keys("noteUserListenedPoi:" + "*");
redisTemplate.delete(keys);

```
