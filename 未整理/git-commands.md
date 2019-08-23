# 常用命令

> HEAD指向的版本就是当前版本，HEAD^ 表示上一个版本，HEAD^^ 表示上上个版本，HEAD~100 表示往上100个版本。

命令 | 描述
---|---
git init	|	初始化一个Git仓库
git add <file>	|	把文件添加到仓库。可以反复多次使用，添加多个文件
git commit -m "description"	|	把文件提交到仓库
git status	|	查看工作区状态
git diff 	|	查看修改内容（查看工作区和暂存区的区别）
git diff --cached	|	查看暂存区和分支的区别
git diff HEAD -- <file>	|	查看工作区和版本库里面最新版本的区别
git log	|	查看提交日志
git log --pretty=oneline	|	查看提交日志（简化日志输出信息）
git reflog	|	查看命令历史
git reset --hard HEAD^	|	版本回退到上一个版本
git reset --hard commit_id	|	版本回退到指定版本
git reset HEAD <file>	|	把暂存区的修改撤销
git checkout -- <file>	|	file文件在工作区的修改全部撤销。让这个文件回到最近一次git commit或git add时的状态
git rm <file>	|	删除文件（相当于 rm <file>，git add <file>）
git remote add origin https://github.com/jiaxiaojiao/learngit.git	|	关联远程仓库
git push -u origin master	|	把本地库的所有内容推送到远程库（第一次推送 加上了-u参数）
git push origin master	|	把本地master分支的最新修改推送至GitHub
git branch	|	查看分支
git branch <name>	|	创建分支
git checkout <name>	|	切换分支
git checkout -b <name>	|	创建+切换分支
git merge <name>	|	合并某分支到当前分支
git merge --no-ff -m <message> <name>	|	强制禁用Fast forward模式，合并某分支到当前分支。
git branch -d <name>	|	删除分支
git log --graph	|	查看分支合并图
git stash	|	把当前的工作现场存储起来。
git stash apply	|	恢复工作现场
git stash drop	|	删除stash内容
git stash pop 	|	恢复工作现场，把stash内容删掉
git branch -D <name>	|	强行删除一个没有被合并过的分支
git remote	|	查看远程库信息
git remote -v	|	查看远程库详细信息
git tag <tagname>	|	新建一个标签，默认HEAD，也可以指定一个commit id
git tag -a <tagname> -m "blabla..."	|	指定标签信息
git tag	|	查看所有标签
git tag -d <tagname>	|	删除标签
git push origin <tagname>	|	推送一个本地标签到远程库
git push origin --tags	|	一次性推送全部尚未推送到远程的本地标签
git push origin :refs/tags/<tagname>	|	标签已经推送到远程，删除远程标签：1，本地删除；2，从远程删除。删除命令也是push。
git config --global color.ui true 	|	让Git显示颜色，会让命令输出看起来更醒目
git check-ignore	|	检查.gitignore
