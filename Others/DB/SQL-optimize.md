# SQL 优化

> 查询语句的优化是SQL效率优化的一个方式，可以通过优化sql语句来尽量使用已有的索引，避免全表扫描，从而提高查询效率。最近在对项目中的一些sql进行优化，总结整理了一些方法。

#### 1. 在表中建立索引，优先考虑where、group by使用到的字段。
 
#### 2. 尽量避免使用select *，返回无用的字段会降低查询效率。如下：
``` text
SELECT * FROM t
``` 
优化方式：使用具体的字段代替*，只返回使用到的字段。
 
#### 3. 尽量避免使用in 和not in，会导致数据库引擎放弃索引进行全表扫描。如下：
```text
SELECT * FROM t WHERE id IN (2,3)
SELECT * FROM t1 WHERE username IN (SELECT username FROM t2)
优化方式：如果是连续数值，可以用between代替。如下：
SELECT * FROM t WHERE id BETWEEN 2 AND 3
如果是子查询，可以用exists代替。如下：
SELECT * FROM t1 WHERE EXISTS (SELECT * FROM t2 WHERE t1.username = t2.username)

```

#### 4. 尽量避免使用or，会导致数据库引擎放弃索引进行全表扫描。如下：
```text
SELECT * FROM t WHERE id = 1 OR id = 3
优化方式：可以用union代替or。如下：
SELECT * FROM t WHERE id = 1
UNION
SELECT * FROM t WHERE id = 3
（PS：如果or两边的字段是同一个，如例子中这样。貌似两种方式效率差不多，即使union扫描的是索引，or扫描的是全表）

```

#### 5. 尽量避免在字段开头模糊查询，会导致数据库引擎放弃索引进行全表扫描。如下：
```text
SELECT * FROM t WHERE username LIKE '%li%'
优化方式：尽量在字段后面使用模糊查询。如下：
SELECT * FROM t WHERE username LIKE 'li%'

```
 
#### 6. 尽量避免进行null值的判断，会导致数据库引擎放弃索引进行全表扫描。如下：
```text
SELECT * FROM t WHERE score IS NULL
优化方式：可以给字段添加默认值0，对0值进行判断。如下：
SELECT * FROM t WHERE score = 0

```
 
#### 7. 尽量避免在where条件中等号的左侧进行表达式、函数操作，会导致数据库引擎放弃索引进行全表扫描。如下：
```text
SELECT * FROM t2 WHERE score/10 = 9
SELECT * FROM t2 WHERE SUBSTR(username,1,2) = 'li'
优化方式：可以将表达式、函数操作移动到等号右侧。如下：
SELECT * FROM t2 WHERE score = 10*9
SELECT * FROM t2 WHERE username LIKE 'li%'

```

#### 8. 当数据量大时，避免使用where 1=1的条件。通常为了方便拼装查询条件，我们会默认使用该条件，数据库引擎会放弃索引进行全表扫描。如下：
```text
SELECT * FROM t WHERE 1=1
优化方式：用代码拼装sql时进行判断，没where加where，有where加and。

```
 
其实，总结起来，大家应该也发现了，就是在查询的时候，要尽量让数据库引擎使用索引。而如何让数据库按我们的意思去使用索引就涉及到扫描参数（SARG）的概念。在数据库引擎在查询分析阶段，会使用查询优化器对查询的每个阶段（如一个带子查询的sql语句就存在不同的查询阶段）进行分析，来决定需要扫描的数据量。如果一个阶段可以被用作扫描参数，那么就可以限制搜索的数据量，从而一定程度上提高搜索效率。

SARG的定义：用于限制搜索的一个操作，因为它通常是指一个特定的匹配，一个值的范围内的匹配或者两个以上条件的AND连接。
 
所以，我们要让我们写的查询条件尽量能够让引擎识别为扫描参数。具体做法，就如前面提到的这些方法。