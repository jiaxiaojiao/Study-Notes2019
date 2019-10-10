## 虚拟机固定IP地址

> VMware中创建的虚拟机，希望能固定IP地址。

### 目录
- 前期准备
    - VMware
    - CentOS操作系统
- 设置步骤
    1. [配置VMware的虚拟网络编辑器](#配置VMware的虚拟网络编辑器)
    2. [设置本地VMnet8参数](#设置本地VMnet8参数)
    3. [配置VMware内虚拟机](#配置VMware内虚拟机)
    4. VMware内虚拟机验证：IP地址，ping外网，ping本机

### 配置VMware的虚拟网络编辑器
1. VMware 页面，点击【编辑】
2. 【虚拟网络编辑器】
3. 【更改设置】
4. 选择【VMnet8】
5. 选择【NAT模式】
6. 设置【子网IP】
7. 点击【NAT设置】，记住【网关IP】

### 设置本地VMnet8参数
1. 本机【网络和Internet设置】
2. 【更改适配器选项】
3. 【VMnet8】右击【属性】
4. 选择【IPv4】
5. 设置【IP地址】和【子网掩码】

### 配置VMware内虚拟机

- 网络配置

    ```text
    cd /etc/sysconfig/network-scripts/
    vi ifcfg-ens33
    ```

- 设置固定IP和网关

    设置 | 值 | 描述
    ---|---|---
    BOOTPROTO | static | 开机协议，有dhcp及static
    ONBOOT | yes | 设置为开机启动
    IPADDR | 192.168.2.101 | 你想要设置的固定IP，192.168.2.2-255之间都可以，请自行验证
    NETMASK | 255.255.255.0 | 子网掩码，不需要修改
    GATEWAY | 192.168.2.1 | 网关，和NAT设置里的网关地址要一样
    DNS1 | 114.114.114.114 | 这个是国内的DNS地址，是固定的

- 重启网络服务

    ```text
    service network restart
    ```
