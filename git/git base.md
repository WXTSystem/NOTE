

1. git init
2. 设置
	git config --global user.name "Your Name"
	git config --global user.email "email@..."
3. git add file1,file2,file3
4. git commit -m "desc"
5. git status 
	查看当前状态
6. git diff
	查看修改内容
7. git log
	查看git提交记录
	--pretty=oneline
8. HEAD表示当前版本 HEAD^就是上一个版本 HEAD^^就是上上个版本
9. 回退 git reset --hard HEAD^
10. 回退之后，git log查不到该版本，可以在之前查到的记录里找到对应的commit id
	git reset --hard commitid(可只写前几位，git会自动去找)
11. git reflog 记录每一次命令
![](https://i.imgur.com/3HBEzva.png)

12. 工作区
	电脑里能看到的目录就是工作区
	其中的.git目录不算工作区，而是Git的版本库

13. 版本库
	暂存区：stage（或者叫index）
	还有git为我们创建的第一个分支master，以及指向master的一个指针叫HEAD

14.	git diff HEAD -- filename
	查看工作区和版本库里最新版本的区别

15. git checkout -- filename
	把文件回到最近一次git commit或git add时的状态

16. git reset HEAD filename
	把暂存区的修改撤销掉

17. git rm filename
	从git中删除文件

18. 误删
	git checkout -- filename

19. git checkout 其实使用版本库里的版本替换工作区的版本

20. 本地仓库内容推送到GitHub仓库
	添加远程库
	git remote add origin(远程库的名字) git@github.com:githubaccount/repname.git

	推送本地内容
	git push -u origin master
	加上-u参数还会把本地的master分支和远程的master分支关联起来

	现在本地作了提交，就可以通过命令
	git push origin master把本地master分支的最新修改推送至GitHub

21. 从远程克隆一个本地库
	git clone git@github.com:githubaccountname/repname.git

# 分支管理 #
1. 创建分支,dev分支（-b表示创建并切换）
	git checkout -b dev
	相当于
	git branch dev
	git checkout dev

2. 查看当前分支
	git branch

3. 切换回master分支
	git checkout master

4. 合并dev分支成果
	git merge dev

	Fast-forward快速合并	
	也就是直接把master指向dev的当前提交

5. 删除dev分支
	git branch -d dev

6. 合并时，有时不能快速合并，使用git status查看冲突的文件

7. git log --graph可以看到分支合并图

8. git merge --no-ff -m "ddd" dev
	禁用fast forward模式，git会在merge时生成一个新的commit，因为快速模式，会直接将master指向分支，删除分之后，会丢失分支的commit信息

9. stash储藏当前现场
	git stash（可以多次stash）
	查看stash git stash list
	恢复
	- 不删除stash git stash apply （可选+stash@{0}恢复到指定stash）
	- 恢复的同时删除stash内容 git stash pop

10. 丢弃一个没有被合并过的分支 -D
	git branch -D name

11. 查看远程仓库信息
	git remote -v

12. 推送本地分支
	git push remotename master
13. 多人协作模式
- 
    因此，多人协作的工作模式通常是这样：
    
    首先，可以试图用git push origin <branch-name>推送自己的修改；
    
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    
    如果合并有冲突，则解决冲突，并在本地提交；
    
    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
    
    如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
    
    这就是多人协作的工作模式，一旦熟悉了，就非常简单。
    

14.rebase
- 
	rebase操作可以把本地未push的分叉提交历史整理成直线；
	
	rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。


# 标签 #
	git tag tagname
	默认标签是打在最新提交的commit上
	在历史log上添加标签
	git tag tagname commitid
	
	删除标签
	git tag -d tagname
	
	推送标签到远程
	git push origin tagname
	
	推送全部标签
	git push origin --tags
	
	删除远程，先删除本地
	git tag -d tagname	
	git push origin :refs/tags/tagname

# 使用GitHub #
	对某个项目感兴趣，fork一下，就会在自己账号下克隆了一个bootstrap仓库，然后可以clone到本地
	
	一些开源项目，你修改后觉得不错，可以在GitHub上发起一个pull request

# 配置别名 #
	git comfig --global alias.st status
	git st 等同于git status
	命令git reset HEAD file可以把暂存区的修改撤销掉（unstage）
	$ git config --global alias.unstage 'reset HEAD'
	$ git unstage test.py


	git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

