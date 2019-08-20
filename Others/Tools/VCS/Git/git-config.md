# 配置


## 用户名和邮箱
> 用户名和邮箱相当于你的身份标示，是本地Git客户端的一个变量，不会随着Git库而改变。
> 每次commit都会使用用户名和邮箱记录。
> GitHub的contributions跟邮箱有关联。

#### 查看用户名和邮箱
```text
  $ git config user.name
  $ git config user.email
```

#### 修改用户名和邮箱
```text
  $ git config --global user.name "jiaxiaojiao"
  $ git config --global user.email "jiaxiaojiao@yahoo.com"
```