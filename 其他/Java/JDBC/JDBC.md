# JDBC 
> Java DataBase Connectivity

> Java 数据库连接。

> 是一种用于执行SQL语句的Java API

## 优点
- 可以为多种数据库提供统一的访问。

## 用途
JDBC 可做三件事：与数据库建立连接、发送 操作数据库的语句并处理结果。


## 通过JDBC访问数据库
1. 加载JDBC驱动器。classpath，WEB-INF/lib
2. 加载JDBC驱动。 Class.forName() 把类加载到JVM中。
3. 建立数据库连接。DriverManager.getConnection(url, username, password);
4. 建立Statement对象 或 PreparedStatement对象。
5. 执行SQL语句。
6. 访问结果集 ResultSet对象
7. 依次将ResultSet，Statement， Connection对象关闭，释放占有的资源。

JDBC驱动在底层 通常都是通过网络IO实现SQL命令与数据传输的。

## 不足
尽管JDBC在JAVA语言层面实现了统一，但不同数据库仍旧有许多差异。

为了更好地实现跨数据库操作，于是诞生了Hibernate项目，Hibernate是对JDBC的再封装，实现了对数据库操作更宽泛的统一和更好的可移植性。

## [to...Hibernate](../Hibernate/Hibernate.md)