## 配置中心

### 目录
- [为什么需要统一配置中心？](#配置中心的必要性)
- [都有那些开源的配置中心？](#开源的配置中心)
- [配置中心对比](#配置中心对比)

- [参考1](https://www.cnblogs.com/xiaoqi/p/configserver-compair.html)
- [参考2](https://www.itcodemonkey.com/article/13646.html)

### 配置中心的必要性

- 统一管理：随着程序的日益复杂，程序的配置也越来越多，公共配置不应该分散于应用中，应该抽离出来集中管理。
- 局限性：对配置的要求也越来越高，动态调整，实时生效，灰度发布等。

[etcd](ETCD.md)和[zookeeper](../Apache/ZooKeeper.md)通常定义为服务注册中心，统一配置中心的事情交给专业的工具去解决。


### 开源的配置中心

1. [Spring Cloud/Spring Cloud Config](../Framework/Spring/Spring-Cloud/Spring-Cloud-Config.md) ※

    GitHub地址： https://github.com/spring-cloud/spring-cloud-config
    
    2014年9月开源，Spring Cloud 生态组件，为分布式系统中的外部配置提供服务器和客户端支持，可以和Spring Cloud体系无缝整合。

2. 携程 Apollo ※

    GitHub地址： https://github.com/ctripcorp/apollo/
    
    Apollo（阿波罗）是携程框架部门研发的分布式配置中心，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性，适用于微服务配置管理场景。
    
    2016年5月，携程开源的配置管理中心，具备规范的权限、流程治理等特性。
    
3. 阿里 Nacos ※

    GitHub地址：https://github.com/alibaba/nacos
    
    一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。
    
    2018年6月，阿里开源的配置中心，也可以做DNS和RPC的服务发现。
    
4. 淘宝diamond

    GitHub地址： https://github.com/takeseem/diamond
    
    已经不维护了。
    
5. Disconf

    GitHub地址： https://github.com/knightliao/disconf
    
    Java开发，蚂蚁金服技术专家发起，业界使用广泛。
    
    2014年7月百度开源的配置管理中心，同样具备配置的管理能力，已经不维护了，GitHub上最近的一次提交是2018年7月26日。
    

### 配置中心对比 功能

功能对比（Nacos具有Apollo大部分功能）

功能点 | Spring Cloud Config | 携程 Apollo | 阿里 Nacos | 备注
---|---|---|---|---
静态配置管理 | 基于file | 支持 | 支持 | --
动态配置管理 | 支持 | 支持 | 支持 | --
统一管理 | 无，需要github | 支持 | 支持 | --
多环境多集群 | 无，需要github | 支持 | 支持 | --
本地配置缓存 | 无 | 支持 | 支持 | --
高可用 | 客户端本地无文件缓存，配置中心宕机，服务无法重启 | 客户端本地缓存，配置中心宕机，服务重启无影响 | 不影响 | --
配置锁 | 支持 | 不支持 | 不支持 | 不允许动态及远程更新
配置校验 | 无 | 支持 | 支持 | 如：ip地址校验，配置
配置生效时间 | 重启生效，或手动refresh生效 | 实时 | 实时 | 需要结合热加载管理， springcloudconfig需要 git webhook+rabbitmq 实时生效
配置更新推送 | 需要手工触发 | 支持 | 支持 | --
配置定时拉取 | 无 | 支持 | 支持 | --
用户权限管理 | 无，需要github | 支持 | 暂不支持 | 现阶段可以人工处理
授权、审核、审计 | 无，需要github | 支持 | 暂不支持 | 现阶段可以人工处理
配置版本管理 | Git做版本管理 | 界面上直接提供发布历史和回滚按钮 | 支持 | --
配置合规检测 | 不支持 | 支持（但还需完善） | 支持 | --
实例配置监控 | 需要结合springadmin | 支持 | 支持 | --
灰度发布 | 不支持 | 支持 | 暂不支持 | 现阶段可以人工处理
告警通知 | 不支持 | 支持，邮件方式告警 | 支持，<br> grafana支持多种告警方式，常用的有邮件，钉钉和webhook方式 | --

总结： Apollo和Nacos相对于Spring Cloud Config的生态支持更广，在配置管理流程上做的更好。Apollo相对于Nacos在配置管理做的更加全面，不过使用起来也要麻烦一些。Nacos使用起来相对比较简洁，在对性能要求比较高的大规模场景更适合。
    
此外，Nacos除了提供配置中心的功能，还提供了动态服务发现、服务共享与管理的功能，降低了服务化改造过程中的难度。

### 配置中心对比 技术路线兼容性

引入配置中心，需要考虑和现有项目的兼容性，以及是否引入额外的第三方组件。我们的java项目以SpringBoot为主，需要重点关注springboot支持性。

功能点 | Spring Cloud Config | 携程 Apollo | 阿里 Nacos
---|---|---|---
SpringBoot支持 | 原生支持 | 支持 | 支持
SpringCloud支持 | 原生支持 | 支持 | 支持
客户端支持 | Java | Java/.Net/Go/C++/Python/PHP/OpenApi | Python/Java/OpenApi/Nodejs
依赖组件 | Eureka | Eureka | 不依赖其他组件

 
### 配置中心对比 可用性与易用性 

引入配置中心后，所有的应用都需要依赖配置中心，因此可用性需要重点关注，另外管理的易用性也需要关注。

功能点 | Spring Cloud Config | 携程 Apollo | 阿里 Nacos
---|---|---|---
单点故障（SPOF） | 支持HA部署 | 支持HA部署 | --
多数据中心部署 | 支持 | 支持 | 支持
单机部署 | Config-Server+Git+Spring Cloud Bus <br> (支持配置实时推送) | Apollo-quickstart+MySQL | Nacos单节点
分布式部署 | 部署复杂 <br> Config-Server(2)+Git+MQ | 部署复杂 <br> Config(2)+Admin(2)+Portal(2)+MySQL | 部署简单 <br> Nacos(3)+MySQL 
配置获取性能 | 较慢，通过git | 快，数据库访问+缓存支持 | 快，性能最好
配置界面 | 无，需要通过git操作 | 统一界面（ng编写） | --

总结： Nacos的部署结构比较简单，运维成本较低。Apollo部署组件较多，运维成本比Nacos高。Spring Cloud Config生产高可用的成本最高。

### 最终选择
综上，目前携程 Apollo 是较好的选择方案，最终选择Apollo。

- 支持不同环境（开发、测试、生产）、不同集群
- 完善的管理系统，权限管理、发布审核、操作审计
- SpringBoot集成友好 ，较小的迁移成本
- 配置修改实时生效（热发布）
- 版本发布管理


### 部署情况

- 管理Web：http://config.***.com/
- 三个环境MetaServer：
    - Dev: config.devmeta.***.com
    - Test: config.testmeta.***.com
    - PRO: config.prometa.***.com
