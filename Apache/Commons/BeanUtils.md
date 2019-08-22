## Apache Commons BeanUtils

网站： https://commons.apache.org/proper/beanutils/

GitHub： https://github.com/apache/commons-beanutils

文档： http://commons.apache.org/proper/commons-beanutils/javadocs/v1.9.4/apidocs/index.html

> BeanUtils provides an easy-to-use but flexible wrapper around reflection and introspection.
> 
> 最新版本： 1.9.4 (Released 2019-08-13)
>
> 主要是用于JavaBean封装数据的操作。

### 目录
- BeanUtils 封装数据
    - [常用方法](#BeanUtils常用方法)
- ConvertUtils 处理类型转换
    - [常用方法](#ConvertUtils常用方法)



### BeanUtils常用方法

- copyProperties(Object dest, Object orig)
    
    Copy property values from the origin bean to the destination bean for all cases where the property names are the same.
    
    对于所有属性名称相同的情况，将属性值从原始bean复制到目标bean。

- populate(Object bean, Map<String,? extends Object> properties)

    Populate the JavaBeans properties of the specified bean, based on the specified name/value pairs.
    
    根据指定的名称/值对填充指定bean的javabean属性。
    
- getProperty(Object bean, String name)
    
    Return the value of the specified property of the specified bean, no matter which property reference format is used, as a String.
    
    获得属性值
    
- setProperty(Object bean, String name, Object value)
    
    Set the specified property value, performing type conversions as required to conform to the type of the destination property.
    
    设置属性值

### ConvertUtils常用方法

