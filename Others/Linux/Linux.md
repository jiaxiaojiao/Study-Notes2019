# Linux 
> Linux 常用指令

## linux CPU大小
```text
cat /proc/cpuinfo |grep "model name" && cat /proc/cpuinfo |grep "physical id"
```

## 内存大小
```text
cat /proc/meminfo |grep MemTotal
```   

## 硬盘大小
```text
fdisk -l |grep Disk
```

## 查看内核/操作系统/CPU信息的linux系统信息命令
```text
uname -a
```

## 查看操作系统版本，是数字1不是字母L
```text
head -n 1 /etc/issue
```

## 查看CPU信息的linux系统信息命令
```text
cat /proc/cpuinfo
```

## 查看计算机名的linux系统信息命令
```text
hostname
```

## 列出所有PCI设备
```text
lspci -tv
```

## 列出所有USB设备的linux系统信息命令
```text
lsusb -tv
```

## 列出加载的内核模块
```text
lsmod
```

## 查看环境变量资源
```text
env 
```

## 查看内存使用量和交换区使用量
```text
free -m
```

## 查看各分区使用情况
```text
df -h
```

## 查看指定目录的大小
```text
du -sh 
```
## 查看内存总量
```text
grep MemTotal /proc/meminfo
``` 

## 查看空闲内存量
```text
grep MemFree /proc/meminfo 
```

## 查看系统运行时间、用户数、负载
```text
uptime 
```

## 查看系统负载磁盘和分区
```text
cat /proc/loadavg 
```

## 查看挂接的分区状态
```text
mount | column -t 
```

## 查看所有分区
```text
fdisk -l 
```

## 查看所有交换分区
```text
swapon -s 
```

## 查看磁盘参数(仅适用于IDE设备)
```text
hdparm -i /dev/hda
```

## 查看启动时IDE设备检测状况网络 
```text
dmesg | grep IDE
```

## 查看所有网络接口的属性 
```text
ifconfig 
```

## 查看防火墙设置
```text
iptables -L 
```

## 查看路由表
```text
route -n 
```

## 查看所有监听端口
```text
netstat -lntp 
```

## 查看所有已经建立的连接
```text
netstat -antp 
```

## 查看网络统计信息进程
```text
netstat -s 
```

## 查看所有进程
```text
ps -ef 
```

## 实时显示进程状态用户
```text
top 
```

## 查看活动用户
```text
w 
```

## 查看指定用户信息
```text
id 
```

## 查看用户登录日志
```text
last 
```

## 查看系统所有用户
```text
cut -d: -f1 /etc/passwd 
```

## 查看系统所有组
```text
cut -d: -f1 /etc/group 
```

## 查看当前用户的计划任务服务
```text
crontab -l 
```

## 列出所有系统服务
```text
chkconfig –list 
```

## 列出所有启动的系统服务程序
```text
chkconfig –list | grep on 
```

## 查看所有安装的软件包
```text
rpm -qa 
```

## 查看CPU相关参数的linux系统命令
```text
cat /proc/cpuinfo 
```

## 查看linux硬盘和分区信息的系统信息命令
```text
cat /proc/partitions 
```

## 查看linux系统内存信息的linux系统命令
```text
cat /proc/meminfo 
```

## 查看版本，类似uname -r
```text
cat /proc/version 
```

## 查看设备io端口
```text
cat /proc/ioports 
```

## 查看中断
```text
cat /proc/interrupts 
```

## 查看pci设备的信息
```text
cat /proc/pci 
```

## 查看所有swap分区的信息
```text
cat /proc/swaps 
```
