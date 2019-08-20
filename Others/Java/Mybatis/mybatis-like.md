# MyBatis中Like语句使用方式

### Oracle

```text
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE CONCAT('%',#{name},'%') 
    
    或 
    
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE '%'||#{name}||'%'

```

### SQL Server

```text
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE '%'+#{name}+'%'

```

### MySQL

```text
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE CONCAT('%',#{name},'%')

```

### DB2

```text
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE CONCAT('%',#{name},'%')
    
    或 
    
    SELECT
    * 
    FROM
    user
    WHERE
    name LIKE '%'||#{name}||'%'

```

### 通用

```text
    SELECT
    * 
    FROM
    user
    WHERE 1 = 1
    <if test="name != null and name != ''">
    <bind name="pattern" value="'%' + _parameter.name + '%'" />
    AND name LIKE #{pattern}
    </if>

```