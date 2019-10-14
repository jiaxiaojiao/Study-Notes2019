## Git

> 分布式版本控制系统。

### 目录


-- 未完...

Git配置

    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"


创建版本库
    
    初始化一个Git仓库
	$ git init
	添加文件到Git仓库
	$ git add <file>
	$ git commit -m "description"

查看工作区状态

    $ git status

查看修改内容

    git diff 可以查看工作区(work dict)和暂存区(stage)的区别
	$ git diff
	
	git diff --cached 可以查看暂存区(stage)和分支(master)的区别
	$ git diff --cached
	
	git diff HEAD -- <file> 可以查看工作区和版本库里面最新版本的区别
	$ git diff HEAD -- <file>

查看提交日志

    $ git log

简化日志输出信息

    $ git log --pretty=oneline

查看命令历史

    $ git reflog

版本回退

    $ git reset --hard HEAD^         回退到上个版本
    $ git reset --hard HEAD~3        回退到前3次提交之前，以此类推，回退到n次提交之前

回退到/进到指定commit的sha码

    $ git reset --hard commit_id

删除文件

    $ git rm <file>

远程仓库

    创建SSH Key
	$ ssh-keygen -t rsa -C "youremail@example.com"
	
	关联远程仓库
	$ git remote add origin https://github.com/username/repositoryname.git
	
	推送到远程仓库
	$ git push -u origin master
	-u 表示第一次推送master分支的所有内容，此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改。

	从远程克隆
	打开指定目录 cd 或在指定目录下右键Git Hash Here
	$ git clone https://github.com/usern/repositoryname.git

分支

    创建分支
	$ git branch <branchname>

	查看分支
	$ git branch
	git branch命令会列出所有分支，当前分支前面会标一个*号。
	
	所有分支
	$ git branch -r
	
	当前远程分支情况
	$ git branch -a

	切换分支
	$ git checkout <branchname>

	创建+切换分支
	$ git checkout -b <branchname>

	合并某分支到当前分支
	$ git merge <branchname>

	删除分支
	$ git branch -d <branchname>

	查看分支合并图
	$ git log --graph
	当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。用git log --graph命令可以看到分支合并图。

	普通模式合并分支
	$ git merge --no-ff -m "description" <branchname>
	因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。合并分支时，加上--no-ff参数就可以用普通模式合并，能看出来曾经做过合并，包含作者和时间戳等信息，而fast forward合并就看不出来曾经做过合并。

保存工作现场

    $ git stash

查看工作现场

    $ git stash list

恢复工作现场

    $ git stash pop

丢弃一个没有合并过的分支

    $ git branch -D <branchname>

查看远程库信息

    $ git remote -v

在本地创建和远程分支对应的分支

    $ git checkout -b branch-name origin/branch-name，
	本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联

    $ git branch --set-upstream branch-name origin/branch-name；

从本地推送分支

    $ git push origin branch-name
	如果推送失败，先用git pull抓取远程的新提交；

从远程抓取分支

    $ git pull
	如果有冲突，要先处理冲突。

标签

tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

新建一个标签
	
	$ git tag <tagname>
	命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id。

指定标签信息
	
	$ git tag -a <tagname> -m <description> <branchname> or commit_id
	git tag -a <tagname> -m "blablabla..."可以指定标签信息。

PGP签名标签
	
	$ git tag -s <tagname> -m <description> <branchname> or commit_id
	git tag -s <tagname> -m "blablabla..."可以用PGP签名标签。

查看所有标签
	
	$ git tag

推送一个本地标签
	
	$ git push origin <tagname>

推送全部未推送过的本地标签
	
	$ git push origin --tags

删除一个本地标签
	
	$ git tag -d <tagname>

删除一个远程标签
	
	$ git push origin :refs/tags/<tagname>



# Git 

```text
    Git是一款开源分布式版本控制系统。
    每个Git工作目录是一个带有完整历史记录和版本信息的仓库，不依赖于网络和中央服务器。
    
    命令文档： https://git-scm.com/docs 
    
    下载地址： https://git-scm.com/downloads
    
    关于Git：  https://git-scm.com/book/zh/v2

```

## Git可视化工具：

- tortoisegit.org

    - 下载地址： download.tortoisegit.org/tgit

## Git初始配置

```text
    点击按钮“Git Bash”或指定目录右击选择“Git Bash Here”
    $ git config --global user.name  "jiaxiaojiao"
    $ git config --global user.email "jiaxiaojiao@yahoo.com"

```

## 指定目录创建仓库

```text
    $ git init
```

## Eclipse配置Git用户名和邮箱（eclipse自带插件）

```text
    Windows > preferences > Team > Git > Configuration
    点击“Add Entry”输入用户名和密码，相当于git
    $ git config --global user.name  "jiaxiaojiao"
    $ git config --global user.email "jiaxiaojiao@yahoo.com"
```



## Git提交代码的五个步骤
```text
    1. 查看代码的修改状态。（cd进入目标工程。 git status）
    
    2. 查看代码的修改内容。（git diff <filename>  如果查看历史修改 git diff <hascode> <hashcode> <filename>）
    
    3. 暂存需要提交的代码。（增加一个需要上传的文件 git add <filename>  删除一个不需要的文件 git rm <filename>  添加全部需要上传的文件 git add --all）
    
    4. 提交已暂存的文件。（git commit    git commit -m <comment>  如果发现有文件漏提或注释有误，使用amend更正 git commit --amend）
    
    5. 同步到服务器。（git push -u origin master）
    
    注：
    1. 同步到服务器前需要把服务器代码同步到本地。（git pull）
    2. 如果执行失败，就按照提示还原有冲突的文件，然后再次尝试同步。（git checkout -- <有冲突的文件路径>）
    3. 同步到服务器。（git puch origin <本地分支名>）
    
```
![Git版本库](../../images/git.png)

## Git与SVN的区别：
1. Git是分布式版本控制系统

    SVN是集中式版本控制系统
    
    也就是说svn版本库是集中放在中央服务器的，而干活的时候，用的都是自己电脑，所以首先要从中央服务器那里得到最新版本，然后干活，干完后，需要把自己做完的活推送到中央服务器，并且必须联网才能干活；git没有中央服务器，每个人的电脑就是一个完整的版本库，这样工作的时候不需要联网，多个人协作工作只需把各自修改的文件推送给对方，就可以互相看到对方的修改。

2. Git把内容按元数据方式存储
    
    SVN按文件方式存储
    
3. Git本地和服务器端结构都很灵活，所有版本都存储在一个目录中，你只需要进行分支的切换即可达到在某个分支工作的效果

    SVN如果你需要在本地试验一些自己的代码，只能本地维护多个不同的拷贝，每个拷贝对应一个SVN服务器地址
    
4. Git可以本地提交代码，Git有利于将一个大任务分解，进行本地的多次提交

    SVN只能在本地进行大量的一次性更改，导致将来合并到主干上造成巨大的风险
    
5. Git的代码日志是在本地的，可以随时查看

    SVN的日志在服务器上的，每次查看日志需要先从服务器上下载下来。
    

## 其他

- Git基本工作原理
- 与SVN对比
- 基本运作流程
- 工程初始化及克隆
- 文件提交
- 分支与常用标签
- 远程仓库管理
- 合并与冲突解决
- Git Flow

--- 

未完

<!-- TOC -->

- [版本控制](#版本控制)
    - [什么是版本控制](#什么是版本控制)
    - [为什么要版本控制](#为什么要版本控制)
    - [本地版本控制系统](#本地版本控制系统)
    - [集中化的版本控制系统](#集中化的版本控制系统)
    - [分布式版本控制系统](#分布式版本控制系统)
- [认识 Git](#认识-git)
    - [Git 简史](#git-简史)
    - [Git 与其他版本管理系统的主要区别](#git-与其他版本管理系统的主要区别)
    - [Git 的三种状态](#git-的三种状态)
- [Git 使用快速入门](#git-使用快速入门)
    - [获取 Git 仓库](#获取-git-仓库)
    - [记录每次更新到仓库](#记录每次更新到仓库)
    - [推送改动到远程仓库](#推送改动到远程仓库)
    - [远程仓库的移除与重命名](#远程仓库的移除与重命名)
    - [查看提交历史](#查看提交历史)
    - [撤销操作](#撤销操作)
    - [分支](#分支)
- [推荐阅读](#推荐阅读)

<!-- /TOC -->

## 版本控制

### 什么是版本控制

版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。 除了项目源代码，你可以对任何类型的文件进行版本控制。

### 为什么要版本控制

有了它你就可以将某个文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态，你可以比较文件的变化细节，查出最后是谁修改了哪个地方，从而找出导致怪异问题出现的原因，又是谁在何时报告了某个功能缺陷等等。

### 本地版本控制系统

许多人习惯用复制整个项目目录的方式来保存不同的版本，或许还会改名加上备份时间以示区别。 这么做唯一的好处就是简单，但是特别容易犯错。 有时候会混淆所在的工作目录，一不小心会写错文件或者覆盖意想外的文件。

为了解决这个问题，人们很久以前就开发了许多种本地版本控制系统，大多都是采用某种简单的数据库来记录文件的历次更新差异。

![本地版本控制系统](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3/本地版本控制系统.png)

### 集中化的版本控制系统

接下来人们又遇到一个问题，如何让在不同系统上的开发者协同工作？ 于是，集中化的版本控制系统（Centralized Version Control Systems，简称 CVCS）应运而生。 

集中化的版本控制系统都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。

![集中化的版本控制系统](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3/集中化的版本控制系统.png)

这么做虽然解决了本地版本控制系统无法让在不同系统上的开发者协同工作的诟病，但也还是存在下面的问题：

- **单点故障：** 中央服务器宕机，则其他人无法使用；如果中心数据库磁盘损坏有没有进行备份，你将丢失所有数据。本地版本控制系统也存在类似问题，只要整个项目的历史记录被保存在单一位置，就有丢失所有历史更新记录的风险。
- **必须联网才能工作：** 受网络状况、带宽影响。

### 分布式版本控制系统

于是分布式版本控制系统（Distributed Version Control System，简称 DVCS）面世了。 Git 就是一个典型的分布式版本控制系统。

这类系统，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。 这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。 因为每一次的克隆操作，实际上都是一次对代码仓库的完整备份。

![分布式版本控制系统](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3/分布式版本控制系统.png)

分布式版本控制系统可以不用联网就可以工作，因为每个人的电脑上都是完整的版本库，当你修改了某个文件后，你只需要将自己的修改推送给别人就可以了。但是，在实际使用分布式版本控制系统的时候，很少会直接进行推送修改，而是使用一台充当“中央服务器”的东西。这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

分布式版本控制系统的优势不单是不必联网这么简单，后面我们还会看到 Git 极其强大的分支管理等功能。

## 认识 Git

### Git 简史

Linux 内核项目组当时使用分布式版本控制系统 BitKeeper 来管理和维护代码。但是，后来开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds）基于使用 BitKeeper 时的经验教训，开发出自己的版本系统，而且对新的版本控制系统做了很多改进。 

### Git 与其他版本管理系统的主要区别

 Git 在保存和对待各种信息的时候与其它版本控制系统有很大差异，尽管操作起来的命令形式非常相近，理解这些差异将有助于防止你使用中的困惑。

下面我们主要说一个关于 Git 其他版本管理系统的主要差别：**对待数据的方式**。

**Git采用的是直接记录快照的方式，而非差异比较。我后面会详细介绍这两种方式的差别。**

大部分版本控制系统（CVS、Subversion、Perforce、Bazaar 等等）都是以文件变更列表的方式存储信息，这类系统**将它们保存的信息看作是一组基本文件和每个文件随时间逐步累积的差异。**

具体原理如下图所示，理解起来其实很简单，每个我们对提交更新一个文件之后，系统记录都会记录这个文件做了哪些更新，以增量符号Δ(Delta)表示。

<div align="center">  
<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3deltas.png" width="500px"/>
</div>

**我们怎样才能得到一个文件的最终版本呢？**

很简单，高中数学的基本知识，我们只需要将这些原文件和这些增加进行相加就行了。

**这种方式有什么问题呢？**

比如我们的增量特别特别多的话，如果我们要得到最终的文件是不是会耗费时间和性能。

Git 不按照以上方式对待或保存数据。 反之，Git 更像是把数据看作是对小型文件系统的一组快照。 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 **快照流**。

<div align="center">  
<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3snapshots.png" width="500px"/>
</div>


### Git 的三种状态

Git 有三种状态，你的文件可能处于其中之一：

1. **已提交（committed）**：数据已经安全的保存在本地数据库中。
2. **已修改（modified）**：已修改表示修改了文件，但还没保存到数据库中。
3. **已暂存（staged）**：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。

由此引入 Git 项目的三个工作区域的概念：**Git 仓库(.git directoty) **、**工作目录(Working Directory)** 以及 **暂存区域(Staging Area)** 。

<div align="center">  
<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3areas.png" width="500px"/>
</div>

**基本的 Git 工作流程如下：**

1. 在工作目录中修改文件。
2. 暂存文件，将文件的快照放入暂存区域。
3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

## Git 使用快速入门

### 获取 Git 仓库

有两种取得 Git 项目仓库的方法。

1. 在现有目录中初始化仓库: 进入项目目录运行  `git init`  命令,该命令将创建一个名为 `.git` 的子目录。
2. 从一个服务器克隆一个现有的 Git 仓库: `git clone [url]` 自定义本地仓库的名字: `git clone [url]` directoryname 

### 记录每次更新到仓库

1. **检测当前文件状态** : `git status`
2. **提出更改（把它们添加到暂存区**）：`git add filename ` (针对特定文件)、`git add *`(所有文件)、`git add *.txt`（支持通配符，所有 .txt 文件）
3. **忽略文件**：`.gitignore` 文件
4. **提交更新:** `git commit -m "代码提交信息"` （每次准备提交前，先用 `git status` 看下，是不是都已暂存起来了， 然后再运行提交命令 `git commit`）
5. **跳过使用暂存区域更新的方式** : `git commit -a -m "代码提交信息"`。 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤。
6. **移除文件** ：`git rm filename`  （从暂存区域移除，然后提交。）
7. **对文件重命名** ：`git mv README.md README`(这个命令相当于`mv README.md README`、`git rm README.md`、`git add README` 这三条命令的集合)

### 推送改动到远程仓库

- 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：·`git remote add origin <server>` ,比如我们要让本地的一个仓库和 Github 上创建的一个仓库关联可以这样`git remote add origin https://github.com/Snailclimb/test.git` 
- 将这些改动提交到远端仓库：`git push origin master` (可以把 *master* 换成你想要推送的任何分支)

  如此你就能够将你的改动推送到所添加的服务器上去了。

### 远程仓库的移除与重命名

- 将 test 重命名位 test1：`git remote rename test test1`
- 移除远程仓库 test1:`git remote rm test1`

### 查看提交历史

在提交了若干更新，又或者克隆了某个项目之后，你也许想回顾下提交历史。 完成这个任务最简单而又有效的工具是 `git log` 命令。`git log` 会按提交时间列出所有的更新，最近的更新排在最上面。

**可以添加一些参数来查看自己希望看到的内容：**

只看某个人的提交记录：

```shell
git log --author=bob
```

### 撤销操作

有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 `--amend` 选项的提交命令尝试重新提交：

```console
git commit --amend
```

取消暂存的文件

```console
git reset filename
```

撤消对文件的修改:

```
git checkout -- filename
```

假如你想丢弃你在本地的所有改动与提交，可以到服务器上获取最新的版本历史，并将你本地主分支指向它：

```
git fetch origin
git reset --hard origin/master
```



### 分支

分支是用来将特性开发绝缘开来的。在你创建仓库的时候，*master* 是“默认的”分支。在其他分支上进行开发，完成后再将它们合并到主分支上。

我们通常在开发新功能、修复一个紧急 bug 等等时候会选择创建分支。单分支开发好还是多分支开发好，还是要看具体场景来说。

创建一个名字叫做 test 的分支

```console
git branch test
```

切换当前分支到 test（当你切换分支的时候，Git 会重置你的工作目录，使其看起来像回到了你在那个分支上最后一次提交的样子。 Git 会自动添加、删除、修改文件以确保此时你的工作目录和这个分支最后一次提交时的样子一模一样）

```console
git checkout test
```

<div align="center">  
<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3切换分支.png" width="500px"/>
</div>

你也可以直接这样创建分支并切换过去(上面两条命令的合写)

```console
git checkout -b feature_x
```

切换到主分支

```
git checkout master
```

合并分支(可能会有冲突)

```java
 git merge test
```

把新建的分支删掉

```
git branch -d feature_x
```

将分支推送到远端仓库（推送成功后其他人可见）：

```
git push origin 
```



## 推荐阅读

- [Git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [图解Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
- [猴子都能懂得Git入门](https://backlog.com/git-tutorial/cn/intro/intro1_1.html)
- https://git-scm.com/book/en/v2

[**返回首页目录**](../README.md)
