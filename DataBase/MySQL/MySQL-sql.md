## 常用SQL

### 目录
- [修改字段类型](#修改字段类型)
- [修改表列名](#修改表列名)
- [修改表名](#修改表名)
- [删除表中的列](#删除表中的列)
- [表中添加列](#表中添加列)
- [IF](#IF)
- [IFNULL](#IFNULL)
- [case when](#case-when)


### 修改字段类型

    ALTER TABLE table_name modify COLUMN column_name datatype;
    ALTER TABLE table_name ALTER COLUMN column_name datatype

### 修改表列名

    ALTER TABLE table_name change COLUMN old_column_name new_column_name datatype;

### 修改表名

    ALTER TABLE old_table_name rename AS new_table_name;

### 删除表中的列

    ALTER TABLE table_name DROP COLUMN column_name;

### 表中添加列

    ALTER TABLE table_name ADD column_name datatype;

### IF
```text
语法：
IF(expr1, expr2, expr3)

expr1条件，条件为true，返回expr2；条件为false， 返回expr3。

```

### IFNULL
```text
语法：
IFNULL(expr1, expr2)

在expr1 的值不为NULL的情况下，返回expr1，否则返回expr2

```

例：
```sql
select ifnull(字段名,0) from 表名;
```


### case when
```text
语法：
case 列名
when 条件 then 结果 
else 其他结构
end 别名

```

