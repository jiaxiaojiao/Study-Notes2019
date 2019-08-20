# Tomcat

## Tomcat 启动

```text
    进入bin目录，点击startup.bat启动。
```

## Tomcat 关闭

```text
    进入bin目录，点击shutdown.bat关闭。
```

### Tomcat 配置

```text
1. 设置 JAVA_HOME 为 JDK安装路径。 
Tomcat就可以根据JAVA_HOME找到JDK，然后启动了。（Tomcat依赖于java）

2. 设置 CATALINA_HOME 为 Tomcat安装路径。
这个环境变量能够让Tomcat在该变量所配置的目录来启动。
可以不配置，如果配置startup.bat根据CATALINA_HOME变量启动Tomcat
设置PATH 添加变量值：%CATALINA_HOME%\lib;%CATALINA_HOME%\bin

3. 配置端口。 进入conf目录，编辑server.xml配置文件。
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />

4. 配置web应用。
<Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true">
在Server.xml的<Host>标签中，添加<Context/>标签
<Context path="/news" docBase="E:\news" />
或放到缺省目录下： 将文件夹放到 Tomcat/webapps下

5. war包发送到webapps下，war文件会自动解压，可以直接被访问。


```

### 端口占用问题

```text
使用命令：
    netstat -ano
    
可以找到占用端口的进程pid，再进入任务管理器，将对应pid的进程关闭。
如果没有找到pid，在属性显示栏右键勾选pid，即可看到

```

### Tomcat 目录结构

```text
bin —— 存放启动和关闭Tomcat的脚本文件。
conf —— 存放Tomcat服务器的各种配置文件。
lib —— 存放Tomcat服务器的支撑jar包。
logs —— 存放Tomcat的日志文件。
temp —— 存放运行时产生的临时文件。
webapps —— web应用所在目录，供外界访问的web资源的存放目录。
work —— Tomcat的工作目录。

```

## Tomcat 原理及架构
> 一个Tomcat中只有一个Server，一个Server可以包含多个Service，一个Service只有一个Container，但是可以有多个Connectors，这是因为一个服务可以有多个连接，如同时提供Http和Https链接，也可以提供向相同协议不同端口的连接
Tomcat中最顶层的容器是Server，代表着整个服务器。

[Tomcat原理及架构](/Tomcat/Theory-1.md)

[Tomcat组成与工作原理](/Tomcat/Theory-2.md)

[Tomcat性能优化（未完）](/Tomcat/Theory-2.md)

