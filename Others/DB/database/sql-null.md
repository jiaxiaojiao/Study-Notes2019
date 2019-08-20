# 函数使用

## SQL查询字段如果为null 则返回0
```sql
-- oracle
select nvl(字段名,0) from 表名;

-- sqlserver
select isnull(字段名,0) from 表名; 

-- mysql
select ifnull(字段名,0) from 表名;

```