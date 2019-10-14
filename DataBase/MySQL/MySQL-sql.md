## 常用SQL

### 目录
- [创建数据库](#创建数据库)
- [删除数据库](#删除数据库)
- [选择数据库](#选择数据库)
- [数据类型](#数据类型)
- [创建数据表](#创建数据表)
- [删除数据表](#删除数据表)
- [插入数据](#插入数据)
- [查询数据](#查询数据)
- [修改字段类型](#修改字段类型)
- [修改表列名](#修改表列名)
- [修改表名](#修改表名)
- [删除表中的列](#删除表中的列)
- [表中添加列](#表中添加列)
- [IF](#IF)
- [IFNULL](#IFNULL)
- [case when](#case-when)


### 创建数据库

    CREATE DATABASE 数据库名;
    
    # 或者 
    CREATE DATABASE IF NOT EXISTS 数据库名 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
    # 作用：  1. 如果数据库不存在则创建，存在则不创建。 2. 指定了编码集
   

### 删除数据库

    drop database <数据库名>;

### 选择数据库

    use 数据库名;

### 数据类型

MySQL支持所有的标准SQL数据类型。

这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。

### 创建数据表

    CREATE TABLE table_name (column_name column_type);

### 删除数据表

    DROP TABLE table_name ;

### 插入数据

    INSERT INTO table_name ( field1, field2,...fieldN )
                           VALUES
                           ( value1, value2,...valueN );

### 查询数据

    SELECT column_name,column_name
    FROM table_name
    [WHERE Clause]
    [LIMIT N][ OFFSET M]

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

