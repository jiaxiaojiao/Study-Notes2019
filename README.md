## 学习笔记

> 工作和学习中遇到的一些问题和总结，希望能够慢慢的成长。

### 目录
- [一些概念](Basic-Concept.md)
- [Java基础](Java/Java.md)
- [多线程](Java/Multi-thread.md)
- [Spring](Spring/Spring.md)
- [Thymeleaf](Thymeleaf.md)  Java模板引擎

持久层框架：
- [MyBatis](MyBatis/MyBatis.md)
- [Hibernate](Hibernate.md)

分布式：
- [Zookeeper](Zookeeper.md)  分布式协调服务
- [R2M](R2M.md)  分布式缓存系统
- [Hadoop](Hadoop.md)  分布式系统基础架构

服务器：
- [Nginx](Nginx.md)  HTTP服务器，代理服务器

[**数据库：**](DataBase/Index.md)
- [Oracle](DataBase/Oracle.md) 关系型数据库，安全可靠
- [MySQL](DataBase/MySQL.md)  关系型数据库，开源
- [SQL Server](DataBase/SQL-Server.md) 关系型数据库，美国微软公司，操作简单。
- [DB2](DataBase/DB2.md) 关系型数据库，美国IBM公司，适用于大型应用系统。
- [Sybase](DataBase/Sybase.md) 关系型数据库，美国Sybase公司，大型数据库系统。
- [Redis](DataBase/Redis.md)  NoSQL Key-Value存储数据库
- [HBase](DataBase/HBase.md)  NoSQL 分布式面向列的数据库
- [MongoDb](DataBase/MongoDb.md) NoSQL 文档型数据库

数据类型：
- [布隆过滤器](Bloom-Filter.md)

设计模式：
- [设计模式](Design-Patterns.md)

工具：
- [Git](Git.md) 分布式版本控制系统
- [Jenkins](Jenkins.md) 自动化部署
- [IDEA使用](IDE/IDEA.md)  Java开发集成环境。

其他：
- [REST](RESTful-API.md)  API设计理论
- [ELK](ELK.md) 日志系统
- [Activiti](Activiti.md)  业务流程管理
- [解决Hash碰撞冲突的方法](Hash.md)
- [Groovy](Groovy.md) 基于JVM的敏捷开发语言
- [其他工具](Tools-Other.md)

 ### 技术栈：
 - 微服务（微服务的划分、粒度）
    
    三种拆分方案：
    - 方案一（新浪微博微服务专家胡忠想）
        1. 从业务维度进行拆分，关联比较密切的业务拆分成一个微服务。
        2. 功能且独立的功能。
    - 方案二（阿里）
        1. 服务拆分要迎合业务的需要。充分考虑业务的独立性和专业性。
        2. 拆分后的维护成本要低于拆分前。
        3. 确保拆分后的服务由相对独立的团队负责维护。
        4. 拆分最有价值的结果是提高了系统的可扩展性
        5. 考虑软件发布频率
    - 方案三（资深技术专家李运华）
        1. 基于业务逻辑
        2. 基于稳定性
        3. 基于可靠性
        4. 基于高性能
 
 - Spring Cloud
 - 集群管理 Hadoop Zookeeper(常用接口, Watch机制)  
 - 数据结构
 - 锁实现，cas原理
 - JVM的垃圾回收机制(垃圾收集，回收算法，)
 - volatile使用场景
 - 持久层框架 MyBatis(源码，缓存，二级缓存，插件原理)
 - 数据库 mysql oracle Redis(底层的实现细节)
 - 消息中间件 Kafka