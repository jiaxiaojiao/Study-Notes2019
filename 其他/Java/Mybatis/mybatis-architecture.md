# MyBatis功能架构

Mybatis功能架构分为三层：

1. API接口层

   提供给外部使用的接口Api，开发人员通过这些本地API来操纵数据库。接口层收到调用请求就会调用数据处理层来完成具体的数据处理。

2. 数据处理层
  
    负责具体的SQL查找、SQL解析、SQL执行和执行结果映射处理等。它主要的目的是根据调用的请求完成一次数据库操作。 

3. 基础支撑层
  
    负责最基础的功能支撑，包括连接管理、事务管理、配置加载和缓存处理，这些都是共用的东西，将他们抽取出来作为最基础的组件。为上层的数据处理层提供最基础的支撑。 
