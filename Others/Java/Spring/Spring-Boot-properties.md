# Spring Boot 配置文件

#### Spring Boot 自定义配置文件

```text
 自定义配置文件 xxx.properties 放到指定位置：src/main/resource 

 加载自定义配置文件，使用注解： @PropertySource("classpath:xxx.properties")
 
 使用配置项，使用注解： @Value("${key}")
 
 
```


> Spring Boot项目中多使用多个配置文件。
> application.properties 是主配置文件，放一些项目通用的配置。
> application-dev.properties 是平常开发的配置，比如数据库连接地址、账号密码等。
> application-prod.properties 是生产环境的配置。
> application-test.properties 是测试环境的配置。

> 可以通过application.properties 中设置 spring.profiles.active=prod/dev/test 来使用application-prod.properties / application-dev.properties / application-test.properties 

数据库配置：
```text
spring.datasource.username=XX
spring.datasource.password=XX
```

## Spring-Boot配置文件数据源配置项

参数	|	介绍
---	|	---
spring.datasource.continue-on-error = false	|	初始化数据库时发生错误时，请勿停止
spring.datasource.data =	|	Data（DML）脚本资源引用
spring.datasource.data-username =	|	执行DML脚本（如果不同）的数据库用户
spring.datasource.data-password =	|	执行DML脚本的数据库密码（如果不同）
spring.datasource.dbcp2.* =	|	Commons DBCP2具体设置
spring.datasource.driver-class-name	|	JDBC驱动程序的完全限定名称默认情况下，根据URL自动检测
spring.datasource.generate-unique-name = false	|	生成随机数据源名称
spring.datasource.hikari.* =	|	Hikari具体设置
spring.datasource.initialize = true	|	使用’data.sql’填充数据库
spring.datasource.jmx-enabled = false	|	启用JMX支持（如果基础池提供）
spring.datasource.jndi-name =	|	数据源的JNDI位置。设置时，类，网址，用户名和密码将被忽略
spring.datasource.name = testdb	|	数据源的名称
spring.datasource.password	|	登录数据库的密码
spring.datasource.platform =所有	|	在架构资源中使用的平台（schema - $ {platform} .sql）
spring.datasource.schema =	|	Schema（DDL）脚本资源引用
spring.datasource.schema-username =	|	数据库用户执行DDL脚本（如果不同）
spring.datasource.schema-password =	|	执行DDL脚本的数据库密码（如果不同）
spring.datasource.separator =;	|	语句分隔符在SQL初始化脚本中
spring.datasource.sql-script-encoding =	|	SQL脚本编码
spring.datasource.tomcat.* =	|	Tomcat数据源特定设置
spring.datasource.type =	|	要使用的连接池实现的完全限定名称。默认情况下，它是从类路径自动检测的
spring.datasource.url	|	数据库的JDBC url
spring.datasource.username	|	登录数据库的用户
spring.datasource.xa.data-source-class-name =	|	XA datasource全限定名
spring.datasource.xa.properties =	|	传递给XA数据源的属性。

