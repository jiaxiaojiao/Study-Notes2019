#### org.springframework.jdbc.CannotGetJdbcConnectionException: Failed to obtain JDBC Connection;

数据库连接的异常，造成原因可能是：

1. 数据源配置错误。

    - url ：设置时区serverTimezone=UTC，高版本mysql 设置useSSL=false。 
    
    - driver-class-name
    
    - username
    
    - password
    
2. 导入的数据库连接表问题。

    - mysql-connector-java 选择高版本的，如5.1.47
