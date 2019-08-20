# 项目管理工具

## Maven
#### Maven是什么？
Maven是项目管理和构建自动化工具。Maven简化和标准化项目建设过程。处理编译，分配，文档，团队协作和其他任务的无缝连接。Maven增加可重用性并负责建立相关的任务。

#### Maven目标
Maven的主要目标是提供开发人员：项目是可重复使用，易维护，更容易理解的一个综合模型。插件或交互的工具，这种生命性的模式。

Maven项目的结构和内容在一个XML文件中声明，pom.xml项目对象模型，是整个Maven系统的基本单元。

最强大的功能就是能够自动下载项目依赖库。

#### Maven安装
1. 安装JDK，配置Windows环境变量“JAVA_HOME”
2. 解压Maven zip，添加Windows环境变量“M2_HOME”，“MAVEN_HOME”，添加到环境变量“PATH”，%M2_HOME%\bin。
3. 验证，mvn -version

#### Maven启用代理访问
在Maven配置文件中设置代理服务器：settings.xml

#### Maven资源库
##### Maven本地资源库
用来存储项目的依赖库。默认为.m2目录文件。
更新Maven本地资源库：{M2_HOME}\conf\setting.xml  localRepository 

##### Maven中央存储库
```text
https://search.maven.org/
```

#### Maven远程库下载
在Maven中，当你声明的库不存在于本地资源库，也不存在于Maven中心存储库，该过程将会停止并将错误信息输出到Maven控制台。
默认情况下Maven从Maven中央存储库中，但是有些库在中央存储，只有在Java.net或JBoss的存储库中能够找到。需要添加Java.net远程仓库 、JBoss远程仓库添加到 pom.xml中。
```text
<project ...>
<repositories>
    <repository>
      <id>java.net</id>
      <url>https://maven.java.net/content/repositories/public/</url>
    </repository>
 </repositories>
</project>

<project ...>
    <repositories>
      <repository>
	<id>JBoss repository</id>
	<url>http://repository.jboss.org/nexus/content/groups/public/</url>
      </repository>
    </repositories>
</project>
```

#### Maven的基本操作
```text
mvn package  构建项目
mvn clean 清理项目。当“mvn clean”执行，在“target”文件夹中的一切都将被删除。
mvn test 执行单元测试
mvn install  打包和部署项目到本地资源库
mvn site 为项目生成信息文档站点
mvn site-deploy  通过WebDAV部署自动生成的文档站点到服务器
mvn tomcat:deploy 以WAR文件部署到Tomcat
```

#### Maven项目目录结构
Maven使用“惯例优于配置”的原则。它要求在没有定制之前，所有的项目都有如下的结构：
这是全世界Maven项目的通用约定。

目录 | 目的
---|---
${basedir} | 存放 pom.xml和所有的子目录
${basedir}/src/main/java | 项目的 java源代码
${basedir}/src/main/resources | 项目的资源，比如说 property文件
${basedir}/src/test/java | 项目的测试类，比如说 JUnit代码
${basedir}/src/test/resources | 测试使用的资源
${basedir}/src/target | 存放编译、打包后的输出文件


#### POM(Project Object Model)
一个项目的所有配置都放置在POM文件中：
一个项目所有的配置都放置在 POM 文件中：定义项目的类型、名字，管理依赖关系，定制插件的行为等等。
在 POM 中，groupId, artifactId, packaging, version 叫作 maven 坐标，它能唯一的确定一个项目。有了 maven 坐标，我们就可以用它来指定我们的项目所依赖的其他项目，插件，或者父项目。一般 maven 坐标写成如下的格式：
```text
groupId:artifactId:packaging:version
```

#### Maven插件
一个目标是一个工作单元，而插件则是一个或者多个目标的集合。比如说Jar插件，Compiler插件，Surefire插件等。从看名字就能知道，Jar 插件包含建立Jar文件的目标， Compiler 插件包含编译源代码和单元测试代码的目标。Surefire 插件的话，则是运行单元测试。
mvn 本身不会做太多的事情，它不知道怎么样编译或者怎么样打包。它把构建的任务交给插件去做。插件定义了常用的构建逻辑，能够被重复利用。这样做的好处是，一旦插件有了更新，那么所有的 maven 用户都能得到更新。
Maven生命周期
生命周期指项目的构建过程，它包含了一系列的有序的阶段 (phase)，而一个阶段就是构建过程中的一个步骤。
插件目标可以绑定到生命周期阶段上。一个生命周期阶段可以绑定多个插件目标。当 maven 在构建过程中逐步的通过每个阶段时，会执行该阶段所有的插件目标。
maven 能支持不同的生命周期，但是最常用的是默认的Maven生命周期 (default Maven lifecycle )。如果你没有对它进行任何的插件配置或者定制的话，那么上面的命令 mvn package 会依次执行默认生命周期中直到包括 package 阶段前的所有阶段的插件目标：
1. process-resources 阶段：resources:resources
2. compile 阶段：compiler:compile
3. process-classes 阶段：(默认无目标)
4. process-test-resources 阶段：resources:testResources
5. test-compile 阶段：compiler:testCompile
6. test 阶段：surefire:test
7. prepare-package 阶段：(默认无目标)
8. package 阶段：jar:jar

#### Maven依赖管理
maven 坐标能够确定一个项目。用Maven坐标来解决依赖关系。在 POM 中，依赖关系是在 dependencies 部分中定义的。我们用 dependencies 定义了对于 junit 的依赖：
```xml
  <dependencies> 
    <dependency> 
      <groupId>junit</groupId> 
      <artifactId>junit</artifactId> 
      <version>3.8.1</version> 
      <scope>test</scope> 
    </dependency> 
  </dependencies> 
```

那这个例子很简单，但是实际开发中我们会有复杂得多的依赖关系，因为被依赖的 jar 文件会有自己的依赖关系。那么我们是不是需要把那些间接依赖的 jar 文件也都定义在POM中呢？答案是不需要，因为 maven 提供了传递依赖的特性。
所谓传递依赖是指 maven 会检查被依赖的 jar 文件，把它的依赖关系纳入最终解决的依赖关系链中。针对上面的 junit 依赖关系

#### Maven库
 maven 默认的远程库(http://repo1.maven.org/maven2) 。这个远程库有 maven 的核心插件和可供下载的 jar 文件。
但是不是所有的 jar 文件都是可以从默认的远程库下载的，比如说我们自己开发的项目。这个时候，有两个选择：要么在公司内部设置定制库，要么手动下载和安装所需的jar文件到本地库。
本地库是指 maven 下载了插件或者 jar 文件后存放在本地机器上的拷贝。在 Linux 上，它的位置在 ~/.m2/repository，在 Windows XP 上，在 C:\Documents and Settings\username\.m2\repository ，在 Windows 7 上，在 C:\Users\username\.m2\repository。当 maven 查找需要的 jar 文件时，它会先在本地库中寻找，只有在找不到的情况下，才会去远程库中找。
运行下面的命令能把我们的 helloworld 项目安装到本地库：

```xml
   $mvn install
```
一旦一个项目被安装到了本地库后，你别的项目就可以通过 maven 坐标和这个项目建立依赖关系。比如如果我现在有一个新项目需要用到 helloworld，那么在运行了上面的 mvn install 命令后，我就可以如下所示来建立依赖关系：

```xml
  <dependency>
      <groupId>com.mycompany.helloworld</groupId>
      <artifactId>helloworld</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency> 

```

- Maven重要指令
- clean complie test package install deploy
- Nexus服务搭建
- Nexus仓库管理
- Nexus使用 上传 配置