## IDEA使用

### 目录
- [快捷键 For Windows](IDEA-shortcut-ForWindows.md)
- [快捷键 For Mac](IDEA-shortcut-ForMac.md)

### 常用快捷键

- Ctrl + F 按照文本的内容查找 本页查找
- Ctrl + Shift + F 按照文本的内容查找 全局查找
- Shift + Shift 搜索类、资源、配置项、方法、路径
- Ctrl + Shift + Enter  自动补全当前语句的分号
- Alt + Enter 处理异常
- Ctrl + / 单行注释
- Ctrl + Shift + /  多行注释
- Ctrl + Alt + O 删除没有用的包

### 自定义代码块/注释

> File - Setting - Editor - File and Code Templates – Class
<br> File - Setting - Editor - Live Templates

- 类注释 class-comment
```text
/**
* @description: ${description}
* @author: v-jiaxiaojiao
* @create: $date$ $time$
*/
```

- 方法注释 method-comment
```text
/**
* @description: $discription$
* @param: $params$
* @return: $return$
* @author: v-jiaxiaojiao
* @create: $date$ $time$
*/
```

### Git的更新/提交/还原

1. 更新。提交自己的项目前必须进行更新。
    
    Git - Repository - Pull...

2. 更新完成。

3. 提交代码。 

    - 红色文件  Add
    - 蓝色文件 Commit File...
    - 绿色 Commit Directory...
	- 勾选需要提交的代码，填写Commit Message，Commit and Push，Push

4. 还原。

    Git – Revert

