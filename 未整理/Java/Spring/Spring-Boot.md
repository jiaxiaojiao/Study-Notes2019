# Spring Boot
> Spring Boot是Spring开源组织下的子项目，也是Spring组件一站式解决方案，主要是为了简化使用Spring框架的难度，简省繁重的配置。

> Spring Boot提供了各种组件的启动器（starters），开发者只要能配置好对应组件参数，Spring Boot就会自动配置，让开发者能快速搭建依赖于Spring组件的Java项目。

> Spring Boot不但能创建传统的war包应用，还能创建独立的不依赖于任何外部容器的独立应用，使用java -jar 命令就能启动。同时，Spring Boot也提供了一个命令行工具来执行Spring的脚本。

> Spring Boot 与传统项目最大的区别就是，传统项目都是打成war包部署到服务器上，需要额外的Servlet 容器，而Spring Boot 则可以直接打成 jar包，并内置集成了 Servlet 容器，通过命令 java -jar xx.jar 就可以直接运行，不需要独立的Servlet 容器。


## Spring Boot优点
- **独立运行** ： 内嵌了各种servlet容器，不需要war包，打可执行的jar包就能独立运行
- **简化配置** ： 启动器自动依赖其他组件，简少了Maven配置。
- **自动配置** ： 自动配置Bean
- **无代码生成和XML配置** ： 借助条件注解
- **应用监控** ： 提供一系列端点可以监控服务和应用
- **上手容易** ： 上手容易 了解核心技术和流程困难，遇到问题棘手。

## 核心配置文件
- **application(.yml .properties)** 
    - 用于Spring Boot项目自动化配置
- **boostrap(.yml .properties)**  
    - 由父ApplicationContext加载，比application优先加载，
    - 属性不能被覆盖
    - 用于使用Spring Cloud Config配置中心时，需要在boostrap配置文件中添加链接到配置中心的配置属性，来加载外部配置中心的配置信息。
    - 用于一些固定的不能被覆盖的属性。
    - 用于一些加密解密的场景。

#### 配置文件格式，书写格式不同。
- .properties
``` text 
app.user.name = javastack
``` 

- .yml
``` text 
app:
    user:
        name:javastack
``` 

#### 配置数据库

```text
在配置文件中添加配置信息：
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/test
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.max-idle=10
spring.datasource.max-wait=10000
spring.datasource.min-idle=5
spring.datasource.initial-size=5

```

## 核心注解

启动类上面的注解是 @SpringBootApplication ，是Spring Boot的核心注解，包含3个注解：
- @SpringBootConfiguration  ，组合了@Configuration 注解，实现配置文件的功能。
- @EnableAutoConfiguration ，打开自动配置的功能，也可以关闭某个自动配置的选项。如关闭数据源自动配置功能 @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
- @ComponentScan ， Spring组件扫描

## Spring Boot常用注解

- [自定义配置文件](Spring-Boot-properties.md) 

- [常用注解](Spring-Boot-annotations.md)

## 开启Spring Boot特性的方式、Spring Boot依赖。
#### 1.  继承 spring-boot-starter-parent 项目
``` text 
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>1.5.6.RELEASE</version>
</parent>
```
#### 2.  导入 spring-boot-dependencies项目依赖。
``` text 
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>1.5.6.RELEASE</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

#### Spring Boot依赖注意：
1. 覆盖属性只对继承有效。修改Spring Boot的依赖组件版本可能会导致不兼容的问题。
2. 资源文件过滤问题。

## 构建Spring Boot的简单实例
- [构建Spring Boot](Spring-Boot-Build.md)

## [关于Spring Boot的几个问题](Spring-Boot-2.md)
