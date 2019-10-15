## Spring Cloud Config

> 配置中心Spring Cloud Config为分布式系统中的外部配置提供服务器和客户端支持。

### 目录
- [Spring Cloud Config服务端特性](#服务端特性)
- [Config客户端的特性（特指Spring应用）](#客户端特性)
- [Spring Cloud Config与其他配置中心对比](../../../Config-Center/Config-Center.md)

### 服务端特性
- HTTP，为外部配置提供基于资源的API（键值对，或者等价的YAML内容）
- 属性值的加密和解密（对称加密和非对称加密）
- 通过使用@EnableConfigServer在Spring boot应用中非常简单的嵌入。

### 客户端特性
- 绑定Config服务端，并使用远程的属性源初始化Spring环境。
- 属性值的加密和解密（对称加密和非对称加密）

