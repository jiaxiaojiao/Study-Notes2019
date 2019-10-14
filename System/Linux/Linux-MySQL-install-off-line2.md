## Linux 离线安装MySQL

> 另一个服务器安装日志。


```text
# 查看系统自带的Mariadb
[root@YZ-222-114-166 local]# rpm -qa|grep mariadb
mariadb-libs-5.5.56-2.el7.x86_64

# 卸载系统自带的Mariadb
[root@YZ-222-114-166 local]# rpm -e --nodeps mariadb-libs 
[root@YZ-222-114-166 local]# rpm -qa|grep mariadb

# 删除etc目录下的my.cnf
没有

# 检查mysql是否存在
[root@YZ-222-114-166 ~]# rpm -qa | grep mysql

# 检查用户和组是否存在
[root@YZ-222-114-166 ~]# cat /etc/group | grep mysql
[root@YZ-222-114-166 ~]# cat /etc/passwd | grep mysql
# 没有用户和组
# 添加组
[root@YZ-222-114-166 ~]# cat /etc/group | grep mysql
mysql:x:1013:
# 添加用户
[root@YZ-222-114-166 ~]# useradd -g mysql mysql
SHTERM: you're not allowed to use this command
# 不能添加，不知道为什么



# 进入/usr/local/文件夹
[root@YZ-222-114-166 ~]# cd /usr/local/
# 上传mysql TAR包
[root@YZ-222-114-166 local]# ls
bin  etc  games  include  info  lib  lib64  libexec  man  mysql-5.7.27-linux-glibc2.12-x86_64.tar.gz  sbin  share  src

# 解压 mysql-5.7.27-linux-glibc2.12-x86_64.tar.gz 
[root@YZ-222-114-166 local]# tar -zxvf mysql-5.7.27-linux-glibc2.12-x86_64.tar.gz 
mysql-5.7.27-linux-glibc2.12-x86_64/bin/myisam_ftdump
mysql-5.7.27-linux-glibc2.12-x86_64/bin/myisamchk
......
mysql-5.7.27-linux-glibc2.12-x86_64/docs/INFO_BIN
mysql-5.7.27-linux-glibc2.12-x86_64/docs/INFO_SRC
[root@YZ-222-114-166 local]# ls
bin  etc  games  include  info  lib  lib64  libexec  man  mysql-5.7.27-linux-glibc2.12-x86_64  mysql-5.7.27-linux-glibc2.12-x86_64.tar.gz  sbin  share  src

# 修改文件夹mysql-5.7.27-linux-glibc2.12-x86_64为mysql
[root@YZ-222-114-166 local]# mv mysql-5.7.27-linux-glibc2.12-x86_64 mysql
[root@YZ-222-114-166 local]# ls
bin  etc  games  include  info  lib  lib64  libexec  man  mysql  mysql-5.7.27-linux-glibc2.12-x86_64.tar.gz  sbin  share  src

# 更改所属的组和用户  没有添加用户mysql
[root@YZ-222-114-166 local]# chown -R mysql mysql/
chown: invalid user: ‘mysql’  
[root@YZ-222-114-166 local]# chgrp -R mysql mysql/
# 修改为了
[root@YZ-222-114-166 local]# chown -R root mysql/


# mysql中，创建data文件夹 没有添加用户mysql，无法授权。
[root@YZ-222-114-166 local]# cd mysql/
[root@YZ-222-114-166 mysql]# ls
bin  COPYING  docs  include  lib  man  README  share  support-files
[root@YZ-222-114-166 mysql]# mkdir data
[root@YZ-222-114-166 mysql]# ls
bin  COPYING  data  docs  include  lib  man  README  share  support-files
[root@YZ-222-114-166 mysql]# chown -R mysql:mysql data
chown: invalid user: ‘mysql:mysql’
# 修改为了
[root@YZ-222-114-166 mysql]# chown -R root:mysql data

# 进入/etc文件夹下 编辑my.cnf
[root@YZ-222-114-166 mysql]# cd /etc/
[root@YZ-222-114-166 etc]# vi my.cnf


# 进入mysql
[root@YZ-222-114-166 etc]# cd /usr/local/mysql/

# 安装mysql. 用户mysql没有添加
[root@YZ-222-114-166 mysql]# bin/mysql_install_db --user=mysql --basedir=/usr/local/mysql/ --datadir=/usr/local/mysql/data/
2019-10-12 14:29:10 [WARNING] mysql_install_db is deprecated. Please consider switching to mysqld --initialize
2019-10-12 14:29:10 [ERROR]   Failed to verify user id 'mysql'. Does it exist?
[root@YZ-222-114-166 mysql]# bin/mysql_install_db --user=root --basedir=/usr/local/mysql/ --datadir=/usr/local/mysql/data/
2019-10-12 14:29:41 [WARNING] mysql_install_db is deprecated. Please consider switching to mysqld --initialize
2019-10-12 14:29:44 [WARNING] The bootstrap log isn't empty:
2019-10-12 14:29:44 [WARNING] 2019-10-12T06:29:41.146651Z 0 [Warning] --bootstrap is deprecated. Please consider using --initialize instead


# 设置文件及目录权限：
[root@YZ-222-114-166 mysql]# cp ./support-files/mysql.server /etc/init.d/mysqld
[root@YZ-222-114-166 mysql]# chmod +x /etc/init.d/mysqld


# 启动mysql
[root@YZ-222-114-166 mysql]# /etc/init.d/mysqld restart
 ERROR! MySQL server PID file could not be found!
Starting MySQL.Logging to '/usr/local/mysql/data/YZ-222-114-166.h.chinabank.com.cn.err'.
2019-10-12T06:32:11.341463Z mysqld_safe Directory '/var/lib/mysql' for UNIX socket file don't exists.
 ERROR! The server quit without updating PID file (/usr/local/mysql/data/YZ-222-114-166.h.chinabank.com.cn.pid).
[root@YZ-222-114-166 mysql]# 

```

还是不行。

太难了，，看日志，原来是没有权限。 赋上权限就好了，，，，

```text
chown -R mysql:mysql /var/data
chown -R mysql:mysql /var/lib/mysql/

```

设置开机启动等，参考上一个。
