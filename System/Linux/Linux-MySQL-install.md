## Linux 安装MySQL

### 目录
- [yum安装 mysql5.7](#YUM安装)
- [离线安装 mysql5.7](Linux-MySQL-install-off-line.md)
- [配置主从](Linux-MySQL-config.md)


### YUM安装
需要提前[安装wget](Linux-install.md#安装wget)命令
1. 下载mysql源安装包
    ```text
    wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    ```

2. 安装mysql源
    ```text
    yum localinstall mysql57-community-release-el7-8.noarch.rpm 
    ```

3. 检查mysql源是否安装成功
    ```text
    yum repolist enabled | grep "mysql.*-community.*"
    ```

4. 安装MySQL 
    ```text
    yum install mysql-community-server
    ```

5. 启动MySQL服务并设置开机启动
    ```text
    systemctl start mysqld
    
    systemctl enable mysqld
    
    systemctl daemon-reload
    ```

6. 端口开放
    ```text
    firewall-cmd --zone=public --add-port=3306/tcp --permanent
    
    firewall-cmd --reload
    ```

7. 修改root本地登录密码
    ```text
    grep 'temporary password' /var/log/mysqld.log
    
    mysql -uroot -p
    
    mysql> set password for 'root'@'localhost'=password('MyNewPass4!'); 
     
    mysql> show variables like '%password%';
    ```

8. 添加远程登录用户
    ```text
    mysql> GRANT ALL PRIVILEGES ON *.* TO 'jiaxiaojiao'@'%' IDENTIFIED BY 'JXJpass-4!' WITH GRANT OPTION;
    ```
