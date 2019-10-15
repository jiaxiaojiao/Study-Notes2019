## 注解

> Spring的注解


- @Autowired
    - 它可以对类成员变量、方法及构造函数进@Component行标注，完成自动装配的工作。 
    - 通过 @Autowired的使用来消除 set、get方法。

- @Component
    - 把普通的POJO实例化到Spring容器中，相当于配置文件的<bean id="" class=""/>
    - 泛指各种组件，当类类不属于各种归类的时候（不属于@Controller、@Services等的时候），我们就可以使用@Component来标注这个类

- @Controller
    - 处理http请求。
    - 标记类为SpringMVC Controller对象，分发处理器将会扫描使用了该注解的类的方法。通俗来说，被Controller标记的类就是一个控制器，这个类中的方法，就是相应的动作。

- @Deprecated
    - 表明这个方法已经过时了

- @Override
    - 标示当前的方法定义将覆盖超类中的方法

- @PathVariable
    - 获取URL中的数据

- @repository
    - DAO层注解
    - 用来标注数据访问层 / 数据访问组件。

- @RequestMapping
    - 配置url映射。
    - @RequestMapping("/hi") 放在类前面用于给整个类设置映射。
    - @RequestMapping(value = {"/hello","/hi"},method = RequestMethod.GET)  放在方法前。

- @ResponseBody
    - @Controller 注解Controller，如果需要返回JSON，XML或自定义mediaType内容到页面，则需要在对应的方法上加上@ResponseBody注解。

- @RestController
    - Spring4之后加入的注解。
    - 相当于@ResponseBody ＋ @Controller
    - 不能返回jsp,html页面。

- @Service
    - getBean的默认名称是类名（头字母小写），可以@Service(“xxxx”)这样来指定
    - 定义的bean默认是单例的，可以使用@Service(“beanName”) @Scope(“prototype”)来改变
    - 可以通过@PostConstruct和@PreDestroy指定初始化方法和销毁方法（方法名任意）
    - 主要用来业务的逻辑处理。

- @SuppressWarnings
    - 忽略编译器警告信息

### 常用的校验注解标签

- @Null  被注释的元素必须为null
- @NotNull  被注释的元素不能为null
- @AssertTrue  被注释的元素必须为true
- @AssertFalse  被注释的元素必须为false
- @Min(value)  被注释的元素必须是一个数字，其值必须大于等于指定的最小值
- @Max(value)  被注释的元素必须是一个数字，其值必须小于等于指定的最大值
- @DecimalMin(value)  被注释的元素必须是一个数字，其值必须大于等于指定的最小值
- @DecimalMax(value)  被注释的元素必须是一个数字，其值必须小于等于指定的最大值
- @Size(max,min)  被注释的元素的大小必须在指定的范围内。
- @Digits(integer,fraction)  被注释的元素必须是一个数字，其值必须在可接受的范围内
- @Past  被注释的元素必须是一个过去的日期
- @Future  被注释的元素必须是一个将来的日期
- @Pattern(value) 被注释的元素必须符合指定的正则表达式。
- @Email 被注释的元素必须是电子邮件地址
- @Length 被注释的字符串的大小必须在指定的范围内
- @NotEmpty  被注释的字符串必须非空
- @Range  被注释的元素必须在合适的范围内

标签注解使用：
1. VO中的字段添加标签
2. Controller中的方法添加@Valid 进行校验
3. Controller中的方法添加参数BindingResult 自定义返回值。
