# Git命令操作

整理自：http://blog.csdn.net/zhang1027963459/article/details/50478340

## 概念：
- 工作区：就是电脑上的目录（未使用git add之前的文件都在工作区）
- 暂存区：就是已经git add但是未git commit
- 版本库：已经git commit，进入版本库中（.git文件夹）

## 命令
### 本地
	git init # 初始化工作区

	echo "test" > test.md
	git add test.md
	git status
	git diff test.md
	git commit -m "first commit"
	git status

	echo "cw" >> test.md # 追加cw字符
	git add test.md
	git status
	git commit -m "second commit"

	git log # 查看版本提交日志
	git reset  –hard HEAD^ 会推倒上1个版本
	git log # 查看版本提交日志
	git reset  –hard HEAD^^ 会推倒上2个版本（两个^）

	git checkout -- test.md # 重新从暂存区里面检出test.md文件

###远程
####本地初始化提交远程
#####概念
本地工作区文件夹内init好一个仓库，然后直接把本地这个仓库环境和远程的关联起来

	ssh-keygen  -t rsa –C "867597730@qq.com" # 必须在bash中运行，CMD里面没有这玩意儿

	git remote add xxx https://github.com/cw1997/studynotes.git # xxx为远程仓库名字，随便起，不一定要是origin，但是前提是这个仓库已经在github上手动new了一个repo

	git push -u xxx master # 拉取别名为xxx的远程仓库中的master主分支

	git checkout -b dev # 创建并且换到dev分支
	git branch dev # 和上面一样的作用

	git branch # 看一下 应该是有master和dev两个分支
	git checkout dev # 切换到dev分支

先在dev分支进行上面本地操作，然后接着测试分至合并
	git checkout master # 确保切换到了master主分支
	git merge dev # 合并dev分支

	git branch -d dev # 删除dev分支
	
	git branch # 看一下 应该是只有master分支了

####远程版本库环境直接克隆到本地
#####概念
本地的工作区文件夹是一个普通文件夹，没有init，所以要直接远程克隆版本库下来

	git clone https://github.com/cw1997/studynotes.git

别人已经推送了新版本库更新，我们由于本地已经有版本库了，所以不要再重复克隆，而是用git pull拉取

	git pull

如果遇到冲突

	git branch --set-upstream dev xxx/dev

这样git pull可以成功，但是并没有合并，我们还要结合下面merge冲突处理解决


### merge冲突处理
出现冲突后：
git merge dev会包merge conflict（合并冲突），Automatic merge failed合并失败，修复冲突再提交

git status会在unmerged paths上报both modified：test.md

再次查看xxx文件，Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中<<<HEAD是指主分支修改的内容，>>>>>test.md

然后我们要经过项目小组讨论之后，再手动处理这个文件，直到没有冲突，然后提交合并。

> 通常合并分支时，git一般使用”Fast forward”模式，在这种模式下，删除分支后，会丢掉分支信息，现在我们来使用带参数 –no-ff来禁用”Fast forward”模式。


### Github上与他人协作开发项目和代码贡献
引用自 https://segmentfault.com/q/1010000009818126

#### 最佳实践
应该是先确保自己仓库的代码已经提交了pull request到对方仓库，而且对方已经merged，之后没有再做其他改动了。那么这个时候可以直接删除我自己Github上的repo，然后重新从源仓库中fork一份来修改，这样是最保险的。**但是这种情况的局限性是：会丢失提交pull request之后所做的修改**

#### 另一种实践
> 首先 把别人的仓库添加到你的上游远程，通常命名为 upstream。操作一次就可以了。

> git remote add upstream 原作者仓库地址
此时再用 git remote -v 就可以看到一个origin是你的，另外一个upstream是原作者的。

> 其次 更新代码

> 使用git fetch upstream 拉去原作者的仓库更新。

> 使用git checkout master 切换到自己的master

> 使用 git merge upstream/master, merge或者rebase到你的master

这种操作是不会丢失pull request之后的修改，而是与现有仓库合并，但是可能出现冲突情况，因为你无法保证你pull request之后的修改和别人在源仓库上的修改代码不会产生冲突。

### 最佳实践
master分支应该是集成测试后的稳定版本分支，dev等分支才是主要干活的分支，而且干活的分支要每个模块一个，一般一个模块里面几个人自己再去协调自己模块分支合并。

master分支合并要全体项目组一起讨论后再操作。




> 因此：多人协作工作模式一般是这样的：
> 
> 首先，可以试图用git push origin branch-name推送自己的修改.
> 如果推送失败，则因为远程分支比你的本地更新早，需要先用git pull试图合并。
> 如果合并有冲突，则需要解决冲突，并在本地提交。再用git push origin branch-name推送。
> Git基本常用命令如下：
> 
>    mkdir：         XX (创建一个空目录 XX指目录名)
> 
>    pwd：          显示当前目录的路径。
> 
>    git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。
> 
>    git add XX       把xx文件添加到暂存区去。
> 
>    git commit –m “XX”  提交文件 –m 后面的是注释。
> 
>    git status        查看仓库状态
> 
>    git diff  XX      查看XX文件修改了那些内容
> 
>    git log          查看历史记录
> 
>    git reset  –hard HEAD^ 或者 git reset  –hard HEAD~ 回退到上一个版本
> 
>                         (如果想回退到100个版本，使用git reset –hard HEAD~100 )
> 
>    cat XX         查看XX文件内容
> 
>    git reflog       查看历史记录的版本号id
> 
>    git checkout — XX  把XX文件在工作区的修改全部撤销。
> 
>    git rm XX          删除XX文件
> 
>    git remote add origin https://github.com/tugenhua0707/testgit 关联一个远程库
> 
>    git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库
> 
>    git clone https://github.com/tugenhua0707/testgit  从远程库中克隆
> 
>    git checkout –b dev  创建dev分支 并切换到dev分支上
> 
>    git branch  查看当前所有的分支
> 
>    git checkout master 切换回master分支
> 
>    git merge dev    在当前的分支上合并dev分支
> 
>    git branch –d dev 删除dev分支
> 
>    git branch name  创建分支
> 
>    git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作
> 
>    git stash list 查看所有被隐藏的文件列表
> 
>    git stash apply 恢复被隐藏的文件，但是内容不删除
> 
>    git stash drop 删除文件
> 
>    git stash pop 恢复文件的同时 也删除文件
> 
>    git remote 查看远程库的信息
> 
>    git remote –v 查看远程库的详细信息
> 
>    git push origin master  Git会把master分支推送到远程库对应的远程分支上

