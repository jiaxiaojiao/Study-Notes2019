## Linux 使用MySQL

### 目录
- [为什么卸载mariadb](#为什么卸载mariadb)
- [进入MySQL数据库](#进入MySQL数据库)


### 为什么卸载mariadb

卸载系统预置的mariadb，才能安装mysql。

原因是：以前的Linux系统中数据库大部分是mysql，不过自从被sun收购之后，就没用集成在centos这些开源Linux系统中了，那么如果想用的话就需要自己安装了，首先centos7 已经不支持mysql，所以内部集成了mariadb，而安装mysql的话会和mariadb的文件冲突，所以需要先卸载掉mariadb


### 进入MySQL数据库

```text
mysql -u root -p
```
