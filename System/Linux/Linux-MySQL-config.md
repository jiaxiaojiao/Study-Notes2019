## Linux 配置MySQL 主从部署

> 前提条件： 
> 1. 至少需要两台服务器。
> 2. 都已安装MySQL数据库

## 目录
1. [Master创建一个同步账户，授权给Slave使用](#Master创建同步账户)
2. [配置Master，启用binlog](#配置Master-启用binlog)
3. [配置Slave， 启用中继日志relay log](#配置Slave-启用relaylog)
4. [配置Slave并启动主从复制](#配置Slave并启动主从复制)
5. [查看Slave服务器状态](#查看Slave服务器状态)
6. [验证，在Master中插入数据，查看Slave是否数据同步](#验证)


数据库角色 | IP | 应用与系统 
---|---|---
Master | 10.222.114.166 | CentOS7 MySQL5.7.27
Slave | 10.222.114.169 | CentOS7 MySQL5.7.27

### Master创建同步账户

Master创建一个同步账户，授权给Slave使用

```text
# 登录MySQL
[root@YZ-222-114-166 ~]# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.27 MySQL Community Server (GPL)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# 创建repl账户
mysql> create user 'repl'@'10.222.114.169' identified by 'replPass!';
Query OK, 0 rows affected (0.00 sec)

# 授权
mysql> grant replication slave on *.* to 'repl'@'10.222.114.169';
Query OK, 0 rows affected (0.00 sec)

# 刷新设置
mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
[root@YZ-222-114-166 ~]# 

```

### 配置Master 启用binlog

配置Master，启用binlog，Master数据库唯一标识，重启MySQL服务

```text
vi /etc/my.cnf

service mysqld restart

ss -antl

# 查看主库的状态
mysql> show master status;
```

修改/etc/my.cnf 内容： 

```text
[mysqld]
basedir = /usr/local/mysql
datadir = /opt/data
socket = /tmp/mysql.sock
port = 3306
pid-file = /opt/data/mysql.pid
user = mysql
skip-name-resolve
//添加以下内容
log-bin=mysql-bin //启用binlog日志
server-id=1 //主数据库服务器唯一标识符 主的必须比从大
log-error=/opt/data/mysql.log

```

详情如下：

```text
# 修改配置：启用binlog，Master数据库唯一标识
[root@YZ-222-114-166 ~]# vi /etc/my.cnf 
# [mysqld]下添加
log-bin=mysql-bin
server-id=1 

# 重启MySQL服务
[root@YZ-222-114-166 ~]# service mysqld restart
Shutting down MySQL.. SUCCESS! 
Starting MySQL. SUCCESS! 
[root@YZ-222-114-166 ~]# ss -antl
State       Recv-Q Send-Q                                 Local Address:Port                                                Peer Address:Port              
LISTEN      0      128                                                *:111                                                            *:*                  
LISTEN      0      511                                                *:80                                                             *:*                  
LISTEN      0      128                                                *:22                                                             *:*                  
LISTEN      0      128                                                *:51899                                                          *:*                  
LISTEN      0      128                                               :::111                                                           :::*                  
LISTEN      0      50                             ::ffff:10.222.114.166:3888                                                          :::*                  
LISTEN      0      65535                                             :::55000                                                         :::*                  
LISTEN      0      64                                                :::6556                                                          :::*                  
LISTEN      0      65535                                             :::18430                                                         :::*                  
LISTEN      0      1024                                              :::59999                                                         :::*                  
LISTEN      0      1024                                              :::60001                                                         :::*                  
LISTEN      0      50                                                :::60002                                                         :::*                  
LISTEN      0      50                                                :::28644                                                         :::*                  
LISTEN      0      1024                                              :::8100                                                          :::*                  
LISTEN      0      50                                                :::2181                                                          :::*                  
LISTEN      0      50                             ::ffff:10.222.114.166:2888                                                          :::*                  
LISTEN      0      90                                                :::3306                                                          :::*                  

# 登录MySQL
[root@YZ-222-114-166 ~]# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.27-log MySQL Community Server (GPL)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# 查询主库的状态
mysql> show master status;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000001 |      154 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)

mysql> exit
Bye
[root@YZ-222-114-166 ~]# 

```

### 配置Slave 启用relaylog

```text
# 配置Slave， 启用中继日志relay log， Slave唯一标识，重启MySQL服务 
[root@YZ-222-114-169 ~]# vi /etc/my.cnf 

# [mysqld] 下面添加
log-error=/usr/local/mysql/data/mysql-error.log
relay-log=mysql-relay-bin
server-id=2

# 重启Slave的MySQL服务
[root@YZ-222-114-169 ~]# service mysqld restart
Shutting down MySQL.. SUCCESS! 
Starting MySQL.Logging to '/usr/local/mysql/data/mysql-error.log'.
 SUCCESS! 
[root@YZ-222-114-169 ~]# ss -antl
State       Recv-Q Send-Q                                 Local Address:Port                                                Peer Address:Port              
LISTEN      0      128                                                *:111                                                            *:*                  
LISTEN      0      128                                                *:22                                                             *:*                  
LISTEN      0      128                                                *:51899                                                          *:*                  
LISTEN      0      511                                                *:8099                                                           *:*                  
LISTEN      0      128                                               :::111                                                           :::*                  
LISTEN      0      50                             ::ffff:10.222.114.169:3888                                                          :::*                  
LISTEN      0      50                                                :::4662                                                          :::*                  
LISTEN      0      65535                                             :::55000                                                         :::*                  
LISTEN      0      64                                                :::6556                                                          :::*                  
LISTEN      0      65535                                             :::18430                                                         :::*                  
LISTEN      0      1024                                              :::59999                                                         :::*                  
LISTEN      0      1024                                              :::60001                                                         :::*                  
LISTEN      0      50                                                :::60002                                                         :::*                  
LISTEN      0      1024                                              :::8100                                                          :::*                  
LISTEN      0      50                                                :::2181                                                          :::*                  
LISTEN      0      90                                                :::3306                                                          :::*                  
[root@YZ-222-114-169 ~]# 

```

修改 /etc/my.cnf 内容如下：

```text
[mysqld]
basedir = /usr/local/mysql
datadir = /opt/data
socket = /tmp/mysql.sock
port = 3306
pid-file = /opt/data/mysql.pid
user = mysql
skip-name-resolve
//添加以下内容：
server-id=2 //设置从库的唯一标识符 从的必须比主小
relay-log=mysql-relay-bin //启用中继日志relay log
error-log=/opt/data/mysql.log
```

### 配置Slave并启动主从复制

```text

# 进入Slave 的MySQL
[root@YZ-222-114-169 ~]# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.27 MySQL Community Server (GPL)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# 配置并启动主从复制
mysql> change master to master_host='10.222.114.166', master_user='repl', master_password='replPass!', master_log_file='mysql-bin.000001', master_log_pos=154;
Query OK, 0 rows affected, 2 warnings (0.02 sec)
```

### 查看Slave服务器状态

```text
# 退出MySQL
mysql> exit
Bye

# 重启服务
[root@YZ-222-114-169 ~]# service mysqld restart
Shutting down MySQL.. SUCCESS! 
Starting MySQL. SUCCESS! 

# 进入Slave的MySQL
[root@YZ-222-114-169 ~]# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.27 MySQL Community Server (GPL)

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# 查看Slave服务器状态。
mysql> show slave status\G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 10.222.114.166
                  Master_User: repl
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000001
          Read_Master_Log_Pos: 154
               Relay_Log_File: mysql-relay-bin.000003
                Relay_Log_Pos: 320
        Relay_Master_Log_File: mysql-bin.000001
             Slave_IO_Running: Yes   # 必须是Yes
            Slave_SQL_Running: Yes   # 必须是Yes
              Replicate_Do_DB: 
          Replicate_Ignore_DB: 
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: 
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 154
              Relay_Log_Space: 527
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
  Replicate_Ignore_Server_Ids: 
             Master_Server_Id: 1
                  Master_UUID: 64b44cfd-ecd1-11e9-8556-f0000ade72a6
             Master_Info_File: /usr/local/mysql/data/master.info
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL
      Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
           Master_Retry_Count: 86400
                  Master_Bind: 
      Last_IO_Error_Timestamp: 
     Last_SQL_Error_Timestamp: 
               Master_SSL_Crl: 
           Master_SSL_Crlpath: 
           Retrieved_Gtid_Set: 
            Executed_Gtid_Set: 
                Auto_Position: 0
         Replicate_Rewrite_DB: 
                 Channel_Name: 
           Master_TLS_Version: 
1 row in set (0.00 sec)

ERROR: 
No query specified

mysql> 
```


### 验证

验证，在Master中插入数据，查看Slave是否数据同步

```text
# 登录Master 
# 创建数据库 data_bus

CREATE DATABASE IF NOT EXISTS data_bus DEFAULT CHARSET utf8 COLLATE utf8_bin;

```
