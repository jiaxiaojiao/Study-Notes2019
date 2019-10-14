## MySQL的日志

> MySQL中主要有binlog、relay log、error log、slow log、operation log、transaction log（undo log、redo log）、general log等日志。
>

### 目录
- [binlog](#binlog)
- [relay log](#relay-log)
- [error log](#error-log)
- [slow log](#slow-log)
- [operation log](#operation-log)
- [transaction log（undo log、redo log）](#transaction-log)
- [general log](#general-log)


### binlog

类似于Oracle的归档日志，可以用来查看数据库的变更历史（具体的时间点所有的SQL操作）、数据库增量备份和恢复（增量备份和基于时间点的恢复）、Mysql的复制（主主数据库的复制、主从数据库的复制）

    mysql>show master status; 查看当前正在使用的二进制日志
    mysql>show binlog events in 'mysql-bin.000001'; 查看二进制日志记录的事件[from position]
    mysql>flush logs; 二进制日志滚动
    mysql>show binary logs; 查看所有二进制日志
    mysql>purge binary logs to 'mysql-bin.000003'; 删除二进制日志

### relay log

中继日志也是二进制日志，用来给slave 库恢复。备库将主库的日志复制到自己的中继日志里。

    relay-log = file_name #指定中继日志的位置和名字，默认为host_name-relay-bin。也可以使用绝对路径，以指定非数据目录来存储中继日志
    relay-log-index = file_name #指定中继日志的名字的索引文件的位置和名字，默认为数据目录中的host_name-relay-bin.index
    relay-log-info-file = file_name #设定中继服务用于记录中继信息的文件，默认为数据目录中的relay-log.info
    relay_log_purge = {ON|OFF} #设定对不再需要的中继日志是否自动进行清理。默认值为ON
    relay_log_space_limit = 0 #设定用于存储所有中继日志文件的可用空间大小。默认为0，表示不限定。最大值取决于系统平台位数
    max_relay_log_size = {4096..1073741824} #设定从服务器上中继日志的体积上限，到达此限度时其会自动进行中继日志滚动。此参数值为0时，mysqld将使用max_binlog_size参数同时为二进制日志和中继日志设定日志文件体积上限

### error log

记录错误信息，告警信息，帮助优化。

    log_error = /mydata/data/mysql.test.com.err #指定错误日志的位置，默认是在数据目录下，这个位置mysql用户必须有写权限
    log_warning = {0|1} #默认开启，服务器运行中的警告日志也会记录在错误日志中

### slow log

慢日志，记录了查询超过限定时间的sql，帮助SQL优化。

    slow_query_log  = {ON | OFF} #是否开启慢慢查询日志，默认是关闭的
    slow_query_log_file = /mydata/data/mysql-slow.log #慢查询日志的存放位置，默认在数据目录下
    log_query_time = 10 #定义默认的时长，默认时长为10秒
    log_query_not_using_indexes = {ON|OFF} #设定是否将没有使用索引的查询操作记录到慢查询日志
    log_output = {TABLE|FILE|NONE} #定义一般查询日志和慢查询日志的保存方式，可以是TABLE、FILE、NONE，也可以是TABLE及FILE的组合(用逗号隔开)，默认为FILE。如果组合中出现了NONE，那么其它设定都将失效，同时，无论是否启用日志功能，也不会记录任何相关的日志信息


### operation log

记录了所有对MySQL请求的信息

    SHOW VARIABLES LIKE "general_log%"; SET GLOBAL general_log = 'ON';

### transaction log

事务日志包括：重做日志redo和回滚日志undo。事务日志用于实例或介质恢复。一般情况下，mysql在崩溃之后，重启服务，innodb通过回滚日志undo将所有已完成并写入磁盘的未完成事务进行rollback，然后redo中的事务全部重新执行一遍即可恢复数据，但是随着redo的量增加，每次从redo的第一条开始恢复就会浪费长的时间，所以引入了checkpoint机制。在系统崩溃重启时，作事务重做；在系统正常时，每次checkpoint时间点，会将之前写入事务应用到数据文件中。

Undo记录的是已部分完成并且写入硬盘的未完成的事务，默认情况下回滚日志是记录下表空间中的（共享表空间或者独享表空间）

Redo记录的是已经全部完成的事务，就是执行了commit的事务，记录文件是ib_logfile0 ib_logfile1

    innodb_data_home_dir = /mydata/data  #InnoDB所有共享表空间数据文件的目录路径，默认在数据目录下
    innodb_data_file_path = ibdata1:1024M  #指定InnoDB的各个数据文件及其大小，文件多于一个时彼此间用分号隔开
    innodb_data_file_path = ibdata2:50M:autoextend  #定义数据大小的增长方式
    innodb_log_group_home_dir = /mydata/data #设定InnoDB重要日志文件的存储目录。在缺省使用InnoDB日志相关的所有变量时，其默认会在数据目录中创建两个大小为5MB的名为ib_logfile0和ib_logfile1的日志文件
    innodb_log_files_in_group = {2 .. 100} #设定日志组中日志文件的个数。InnoDB以循环的方式使用这些日志文件。默认值为2
    innodb_log_file_size = {108576 .. 4294967295} #设定日志组中每个日志文件的大小，单位是字节，默认值是5MB。较为明智的取值范围是从1MB到缓存池体积的1/n，其中n表示日志组中日志文件的个数。日志文件越大，在缓存池中需要执行的检查点刷写操作就越少，这意味着所需的I/O操作也就越少，然而这也会导致较慢的故障恢复速度
    innodb_log_buffer_size = {262144 .. 4294967295} #设定InnoDB用于辅助完成日志文件写操作的日志缓冲区大小，单位是字节，默认为8MB。较大的事务可以借助于更大的日志缓冲区来避免在事务完成之前将日志缓冲区的数据写入日志文件，以减少I/O操作进而提升系统性能。因此，在有着较大事务的应用场景中，建议为此变量设定一个更大的值


### general log

审计：哪个账号、在哪个时段、做了哪些事情。

数据库访问量很大，想要从SQL方面进行优化，因为为了性能考虑，一般general log不会开启。

slow log可以定位一些有性能问题的sql，而general log会记录所有的SQL。

    log = {ON|OFF} #是否启用查询日志，该指令在mysq5.6中已废弃
    general_log = {ON|OFF} #启动或关闭查询日志，默认是关闭的
    general_log_file = /mydata/data/mysql.log #指定查询日志的位置，默认在数据目录下
    log_output = {TABLE|FILE|NONE} #指定存放查询日志的位置，可以放在文件中，也可以放在数据库的表中，放在表中比放在文件中更容易查看

