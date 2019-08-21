# SQL

#### IF
```text
语法：
IF(expr1, expr2, expr3)

expr1条件，条件为true，返回expr2；条件为false， 返回expr3。

```




#### IFNULL
```text
语法：
IFNULL(expr1, expr2)

在expr1 的值不为NULL的情况下，返回expr1，否则返回expr2

```

例：
```sql
select ifnull(字段名,0) from 表名;
```


#### case when
```text
语法：
case 列名
when 条件 then 结果 
else 其他结构
end 别名

```
