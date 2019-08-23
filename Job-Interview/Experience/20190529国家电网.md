# 面试题 

> 国网外包

研发中心-初、中级开发工程师笔试题（外包人员）

Java 笔试题

#### 1. MySQL 或者 Oracle 、 zookeeper 、 Redis默认访问端口是多少？ 

关系型数据库

名称 | 默认端口号 
--- | --- 
MySQL | 3306  
Oracle | 1521  
SQLServer | 1433  
DB2 | 5000 
PostgreSQL | 5432

NoSQL数据库

名称 | 默认端口号 
--- | --- 
Redis | 6379
MongoDB | 27017
memcached | 11211

其他

名称 | 端口 | 说明 
--- | --- | --- 
ZooKeeper | 2181 | 对客户端提供服务的端口
ZooKeeper | 2888 | 集群内机器通讯使用（Leader监听此端口）
ZooKeeper | 3888 | 选举leader使用

#### 2. 写出尽可能多用过的相关注解

注解Annotation | 说明 
--- | --- 
@Deprecated | 这个方法已经废弃了，不建议使用了。 JDK自带注解
@Override | 重写(覆盖)。 JDK自带注解
@SuppressWarnings | 编译器不会针对指定的一个或多个原因产生警告

未完。。。

#### 3. 画图描述一下最熟悉的工程结构是什么样子的？
```text
包按层次结构组织，让组织结构更加清晰。
然后再按特征组织，把相关性的一项放到一个目录

- Controller 
- Service 
- model
- dao
- util

```

#### 4. 列举一下使用过的jar包
```text
commons-beanutils.jar  提供对java反射和自省API的包装  对bean操作的类，可以访问类的属性及get和set方法

commons-digester.jar  Digester基于规则的XML文档解析，主要用于XML到java对象的映射

commons-lang.jar  包含了一些数据类型工具类，是java.lang.* 的扩展  必须使用的包

ant.jar  Ant编译工具的jar包，用来编译Hibernate源代码的。如果你不准备修改和编译Hibernate源代码，那么就没有什么用，可选的jar包

optional.jar  Ant的一个辅助包。

log4j.jar  日志包，可以更加详细的记录日志。可选的。

apache commons  涵盖了大量的小工具，比如发邮件(线上告警用)，快速且方便的IO操作封装。

maven



```

#### 5. 列举一下熟悉的数据库连接池有哪些？
（https://www.open-open.com/project/tag/shuju-lianjiechi.html   https://blog.csdn.net/qq_25406669/article/details/80222376）

主流的数据库连接池（connection pool）： 

Java中常用的数据库连接池有： DBCP、Tomcat Jdbc Pool、BoneCP、Druid、C3P0等

 
#### 6. 如何配置JDK的环境变量
```text
JAVA_HOME  JDK安装目录
Path  %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
CLASSPATH  .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar

```


#### 7. 编写一个SQL查询，获取Employee(Id, Salary字段) 表中第二高的薪水（Salary）。
```sql
select IFNULL( 
    (select DISTINCT salary 
    from employee 
    ORDER BY salary 
    DESC LIMIT 1,1), null
) as "SecondHighestSalary" 

```

#### 8. 假设场景，对方的数据库有100万条数据，需要同步到我方的数据库中。如何实现，有哪几种办法？

```text
Spring boot 配置两个数据库dataSources、SqlSessionFactory

数据库A select ， 数据库B insert 



```
