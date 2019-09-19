## Mapper中传入参数parameterType类型

### 目录
- [parameterType分类](#分类)
- [获取参数中的值](#获取参数中的值)
- [注解@Param](#注解)
- [自定义SQL参数化](#自定义SQL参数化)

### 分类
Mapper中传入参数parameterType分为两种：
1. 基本数据类型。
    - int 
    - string / java.lang.String
    - long / java.lang.Long
    - Date 
2. 复杂数据类型。
    - 类
    - Map / java.util.Map

### 获取参数中的值
1. 基本数据类型： #{参数} 
2. 复杂数据类型： #{属性名} map则是#{key}

### 注解
注解 @Param：
1. 注解单一属性。
    ```text
    #{ @Param中的参数内容}
    ```
2. 注解JavaBean。
    ```text
    #{JavaBean名称.属性名}
    ```

### 自定义SQL参数化

map参数，传入完整sql及sql参数。

1. Mapper.xml
    ```text
      <select id="selectDataBySqlParams" parameterType="java.util.Map" resultType="java.util.LinkedHashMap">
        <![CDATA[ ${sql} ]]>
      </select>
    ```
2. Mapper
    ```text
      List<Map<String, Object>> selectDataBySqlParams(Map<String, Object> params);
    ```
3. 调用
    ```text
      Map<String, Object> params = new HashMap<>();
      String sql = "select * from tb_name where id < #{id}"
      params.put("sql", sql);
      params.put("id", 10);
      List<Map<String, Object>> maps = db.selectDataBySqlParams(params);
    ```
