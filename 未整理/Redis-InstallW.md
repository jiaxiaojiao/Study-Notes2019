# Windows下安装Redis

### 1. 获取安装包

地址： [https://github.com/MicrosoftArchive/redis](https://github.com/MicrosoftArchive/redis)

```text
 => 点击【releases】 进入下载页面 
 => 下载最后发行的版本（如3.2.100）
        Redis-x64-3.2.100.msi  微软格式的安装包
        Redis-x64-3.2.100.zip  压缩包
 
```

### 2. 安装

```text
 => 双击msi文件进行安装
 => 同意协议
 => 指定安装目录
 => 设置端口
 => 指定最大值(Set the Max Mermory limit)

```

### 3. 配置

- 设置密码

```text
文件： redis.windows-service.conf 作为服务运行的Redis配置文件
插入： requirepass下插入 requirepass password

```

- 启动服务

```text
 => 开始
 => 右击计算机
 => 选择管理
 => 计算机管理
 => 服务和应用程序
 => Redis 

```

- 使用客户端程序访问

```text
 => cmd 进入Redis目录
 => redis-cli 客户端程序
 => author password 验证密码（redis.windows-service.conf中设置的密码）

```
