## Git

分布式版本控制系统。

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

    $ git reset --hard HEAD^

回退指定版本号

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


[**返回首页目录**](README.md)