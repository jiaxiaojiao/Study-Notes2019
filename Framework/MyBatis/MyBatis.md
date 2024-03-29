## MyBatis

> 持久层框架。	

中文文档： https://mybatis.org/mybatis-3/zh/index.html 

### 目录
- [描述](#描述)
- [动态SQL](#动态SQL)
    - [Mapper中传入参数parameterType类型](MyBatis-parameterType.md)
    - [自定义SQL参数化-map的扩展](MyBatis-parameterType.md#自定义SQL参数化)
- [缓存](#缓存)
- [插件开发](#插件开发)
- [Spring 集成MyBatis](#Spring-集成MyBatis)
- [Spring Boot集成MyBatis](#Spring-Boot集成MyBatis)
- [添加记录时获取到记录主键id](#添加记录时获取到记录主键id)
- [MyBatis Generator代码自动生成工具](Mybatis-Generator.md)
- [MyBatis源码分析](MyBatis-Code.md)

### 描述

MyBatis原来是Apache的开源项目iBatis(internet abatis), 2010年迁移到Google Code改名为MyBatis，2013年11月迁移到GitHub。
	
MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

### 动态SQL

### 缓存

一级缓存

二级缓存： 二级缓存是Application级别的缓存，可以提高对数据查询的效率。

### 插件开发

### Spring 集成MyBatis

### Spring Boot集成MyBatis

### 添加记录时获取到记录主键id

必须在<insert>的xml配置中添加3个属性：
```text
<insert useGeneratedKeys="true" keyProperty="id" keyColumn="id"></insert>
```
- useGeneratedKeys：必须设置为true，否则无法获取到主键id。
- keyProperty：设置为POJO对象的主键id属性名称。
- keyColumn：设置为数据库记录的主键id字段名称。

新添加主键id并不是在执行添加操作时直接返回的，而是在执行添加操作之后将新添加记录的主键id字段设置为POJO对象的主键id属性。通过访问POJO对象的主键id属性即可返回。
