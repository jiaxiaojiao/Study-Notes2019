# Spring Boot 注解

## @controller
    
    控制器（注入服务）。
    
    用于标注控制层，相当于struts中的action层。

## @RestController

    是@Controller和@ResponseBody的合集,表示这是个控制器bean,并且是将函数的返回值直接填入HTTP响应体中,是REST风格的控制器。

    
## @service 

    服务（注入dao）。
    
    用于标注服务层，主要用来进行业务的逻辑处理
    
## @repository

    （实现dao访问）。
    
    用于标注数据访问层，也可以说用于标注数据访问组件，即DAO组件.

## @SpringBootApplication
    
    包含了@ComponentScan、@Configuration和@EnableAutoConfiguration注解。
    
    其中@ComponentScan让spring Boot扫描到Configuration类并把它加入到程序上下文。
    
## @ComponentScan

    组件扫描，可自动发现和装配一些Bean。    

## @Configuration
    
    等同于spring的XML配置文件；使用Java代码可以检查类型安全。
    
    底层是含有@Component ，所以@Configuration 具有和 @Component 的作用。
    
    可理解为用spring的时候xml里面的<beans>标签。

```text
@Configuration标注在类上，相当于把该类作为spring的xml配置文件中的<beans>，作用为：配置spring容器(应用上下文)

package com.dsx.demo;

import org.springframework.context.annotation.Configuration;

@Configuration
public class TestConfiguration {
    public TestConfiguration() {
        System.out.println("TestConfiguration容器启动初始化。。。");
    }
}
```    
    
相当于：

```text
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context" xmlns:jdbc="http://www.springframework.org/schema/jdbc"  
    xmlns:jee="http://www.springframework.org/schema/jee" xmlns:tx="http://www.springframework.org/schema/tx"
    xmlns:util="http://www.springframework.org/schema/util" xmlns:task="http://www.springframework.org/schema/task" xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
        http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-4.0.xsd
        http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-4.0.xsd
        http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
        http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-4.0.xsd
        http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd" default-lazy-init="false">


</beans>

```    
    
## @component 
    
    （把普通pojo实例化到spring容器中，相当于配置文件中的<bean id="" class=""/>）
    
    泛指各种组件，就是说当我们的类不属于各种归类的时候（不属于@Controller、@Services等的时候），我们就可以使用@Component来标注这个类。

    @Component可配合CommandLineRunner使用，在程序启动后执行一些基础任务。
## @Bean
    
    相当于用spring的时候xml里面的<bean>标签。  
    
    作用是注册bean对象。
    
```text
@Bean标注在方法上(返回某个实例的方法)，等价于spring的xml配置文件中的<bean>，作用为：注册bean对象

package com.dsx.demo;

public class TestBean {

    private String username;
    private String url;
    private String password;

    public void sayHello() {
        System.out.println("TestBean sayHello...");
    }

    public String toString() {
        return "username:" + this.username + ",url:" + this.url + ",password:" + this.password;
    }

    public void start() {
        System.out.println("TestBean 初始化。。。");
    }

    public void cleanUp() {
        System.out.println("TestBean 销毁。。。");
    }
}
```

配置类
```text
package com.dsx.demo;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@Configuration
public class TestConfiguration {
    public TestConfiguration() {
        System.out.println("TestConfiguration容器启动初始化。。。");
    }

    // @Bean注解注册bean,同时可以指定初始化和销毁方法
    @Bean
    @Scope("prototype")
    public TestBean testBean() {
        return new TestBean();
    }
}
```      

上述操作相当于实例化TestBean ，并交给spring管理。

注： 
(1)、@Bean注解在返回实例的方法上，如果未通过@Bean指定bean的名称，则默认与标注的方法名相同； 
(2)、@Bean注解默认作用域为单例singleton作用域，可通过@Scope(“prototype”)设置为原型作用域； 
(3)、既然@Bean的作用是注册bean对象，那么完全可以使用@Component、@Controller、@Service、@Repository等注解注册bean（在需要注册的类上加注解），当然需要配置@ComponentScan注解进行自动扫描。

```text
@Target({ElementType.METHOD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Bean {
    @AliasFor("name")
    String[] value() default {};

    @AliasFor("value")
    String[] name() default {};

    Autowire autowire() default Autowire.NO;

    String initMethod() default "";

    String destroyMethod() default "(inferred)";
}
```

使用@Bean注解时，可以配置initMethod()和destoryMethod方法，分别在实例化和销毁的时候执行。

或者使用通过@PostConstruct 和 @PreDestroy 方法 实现初始化和销毁bean之前进行的操作 。

## @EnableAutoConfiguration
    
    自动配置。

## @Autowired

    自动导入。

## @PathVariable

    获取参数。

## @JsonBackReference

    解决嵌套外链问题。

## @RepositoryRestResourcepublic

    配合spring-boot-starter-data-rest使用。