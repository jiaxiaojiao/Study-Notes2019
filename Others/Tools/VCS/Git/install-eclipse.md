# Eclipse 使用Git

## 安装Git插件
> 安装Git插件，和安装一般插件过程一样。有的Eclipse已经自带Git插件，就不用安装了。

```text
  步骤：
  > Help 
  > Install new software 
  > Add Repository
  
  Name: git
  Location: http://download.eclipse.org/egit/updates/
```

## Git插件卸载
```text
  > Help
  > About Eclipse 
  > Installation Details 
  > Uninstall...
  
```

## 配置用户名和邮箱
```text
  > Window 
  > Preferences 
  > Team 
  > Git 
  > Configuration 
  > User Settings
  
  添加email & name. Add Entry
```

## 连接公司私有Git服务器

#### Git服务器访问的URL、账户以及密码。
- Eclipse生成SSH秘钥 
```text
  > Window 
  > Preference 
  > General 
  > Network Connections 
  > SSH2 
  > Key Management 
  > Generate RSA KEY 
  > Save private key
  
```
 
- 服务器设置，打开GitHub的配置，将SSH2的验证码拷贝。
```text
  拷贝（C:\用户...\.ssh）id_rsa.pub中的内容，粘贴到GitHub 
  > SSH and GPG keys 
  > New SSH key
```
 
#### 使用Import同步到本地仓库（创建本地仓库、引入到工作空间）
```text
  > File 
  > Import 
  > Git 
  > Projects from Git 
  > Existing local repository (如果本地有仓库，有代码，选择)
  > Clone URI(如果第一次使用，没有仓库，选择)
  > URI,User,Password... 
  > Next 
  > Next 
  > 选择Directory,Next
  > 选择项目进入到自己的工作空间。
```

#### 修改的文件提交到本地
pull 从服务器获取代码和本地同步。