## Spring Boot 项目连接数据库-与MyBatis集成

### 前提条件

1. 数据库，数据库表

    ```text
    CREATE TABLE `test` (
      `id` bigint(20) NOT NULL,
      `name` varchar(40) COLLATE utf8_bin DEFAULT NULL,
      `age` int(11) DEFAULT NULL,
      `remark` varchar(40) COLLATE utf8_bin DEFAULT NULL,
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
    ```

### 配置步骤

1. 引入starter
    ```text
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.1.0</version>
    </dependency>
    ```
2. 配置application.properties
    ```text
    spring.datasource.url=jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC
    spring.datasource.driver-class-name=com.mysql.jdbc.Driver
    spring.datasource.username=jiaxiaojiao
    spring.datasource.password=jiaxiaojiao
    
    mybatis.mapper-locations=classpath:mybatis/*.xml
    mybatis.type-aliases-package=com.jocelyn.demo.mapper
    ```
3. POJO
    ```text
    package com.jocelyn.demo.mapper;
    
    import lombok.Data;
    
    /**
     * @description: 测试POJO
     * @author: v-jiaxiaojiao
     * @create: 2019/08/12 10:24
     */
    @Data
    public class Test {
        private Long id; // 主键ID
        private String name; // 名称
        private Integer age; // 年龄
        private String remark; // 备注
    }
    ```
4. Mapper接口
    ```text
    package com.jocelyn.demo.mapper;
    
    import org.apache.ibatis.annotations.Mapper;
    
    /**
     * @description: Test Mapper
     * @author: v-jiaxiaojiao
     * @create: 2019/08/12 10:37
     */
    @Mapper
    public interface TestMapper{
        public int insert(Test test);
    }
    ```
5. Mapper xml
    ```text
    <?xml version="1.0" encoding="utf-8" ?>
    <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="com.jocelyn.demo.mapper.TestMapper">
        <resultMap id="BaseResultMap" type="com.jocelyn.demo.mapper.Test">
            <id column="id" jdbcType="BIGINT" property="id" />
            <result column="name" jdbcType="VARCHAR" property="name"/>
            <result column="age" jdbcType="INTEGER" property="age"/>
            <result column="remark" jdbcType="VARCHAR" property="remark"/>
        </resultMap>
        <sql id="Base_Column_List">
            id, name, age, remark
        </sql>
        
        <insert id="insert" parameterType="com.jocelyn.demo.mapper.Test">
            insert into test(id, name, age, remark)
            values(#{id, jdbcType=BIGINT},
                #{name, jdbcType=VARCHAR},
                #{age, jdbcType=INTEGER},
                #{remark, jdbcType=VARCHAR}
            )
        </insert>
    </mapper>
    ```
6. 编写Controller，Service，Service Impl
    ```text
    package com.jocelyn.demo.controller;
    
    import com.jocelyn.demo.mapper.Test;
    import com.jocelyn.demo.service.TestService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.ResponseBody;
    
    /**
     * @description: 测试Controller
     * @author: v-jiaxiaojiao
     * @create: 2019/08/12 10:53
     */
    @RequestMapping("/test")
    @Controller
    public class TestController {
    
        @Autowired
        public TestService testService;
    
        @ResponseBody
        @RequestMapping("/addTest")
        public String addTest(Test test){
            return testService.addTest(test);
        }
    }
    
    ```
    
    ```text
    package com.jocelyn.demo.service;
    
    import com.jocelyn.demo.mapper.Test;
    
    public interface TestService {
        public String addTest(Test test);
    }
    
    ```
    
    ```text
    package com.jocelyn.demo.service.impl;
    
    import com.jocelyn.demo.mapper.Test;
    import com.jocelyn.demo.mapper.TestMapper;
    import com.jocelyn.demo.service.TestService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    
    /**
     * @description: 测试Service实现
     * @author: v-jiaxiaojiao
     * @create: 2019/08/12 10:57
     */
    @Service
    public class TestServiceImpl implements TestService {
    
        @Autowired
        private TestMapper testMapper;
    
        @Override
        public String addTest(Test test) {
            int i = testMapper.insert(test);
            return "返回值：" + i;
        }
    }
    
    ```

### 测试调用

    ```text
    http://127.0.0.1:8080/test/addTest?name=name1&age=2&remark=测试name1&id=1
    
    返回值：1
    ```



