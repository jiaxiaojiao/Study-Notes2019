# MyBatis 

基于Java的持久层框架，

提供的持久层框架包括 SQL Maps 和 Data Access Objects (DAO)。

消除了几乎所有JDBC代码和参数的手工设置以及结果集的检索。

使用简单的XML 或注解用于配置和原始映射，将接口和Java的POJOs普通的Java对象映射成数据库中的记录。

####  1. #{}和${}的区别是什么？
```text
#{}是预编译处理，${}是字符串替换。
Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；
Mybatis在处理${}时，就是把${}替换成变量的值。
使用#{}可以有效的防止SQL注入，提高系统安全性。
```

#### 2. 分页

#### 3. 设置缓存

#### 4. mybatis 跟 hibernate、 jdbc 的区别 优缺点


# Mybatis
> Mybatis基于Java的持久层框架，支持定制化SQL、存储过程以及高级映射。

> MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Old Java Objects,普通的 Java对象)映射成数据库中的记录。

## 安装

- [Mybatis安装](mybatis-install.md)

## 使用

- [Mybatis中like语句的使用方式](mybatis-like.md)

- [XML文件中的大于小于等于](mybatis-xml.md)

- [XML文件中动态SQL，if判断](mybatis-xml-if.md)

## 架构

- [Mybatis功能架构](mybatis-architecture.md)

## 优缺点

- [Mybatis的优点和缺点](mybatis-advantages.md )


## 其他
```text
Mybatis XML配置
mybatis是如何管理session和cache的
MyBatis3简介
MyBatis3 SqlMap哪些事儿
数据库连接池
MyBatis3 SessionFactory实现原理
MyBatis3 配置文件详解
MyBatis3 事务管理与集成
浅谈Hibernate
MyBatis3 与 Hibernate框架对比

```
