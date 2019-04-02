## Git笔记
### Git结构：
- 三层结构：
	- working directory 工作区
	- staging index 暂存区
	- git directory（Repository）版本库

### 常用命令
- git init 初始化仓库
- git add filename 将项目提交到暂存区
- git commit -m '描述'  将项目提交到本地仓库
- git commit -am ‘描述’ 提交修改的文件，直接跳过缓存区
- git status 查看git内文件的状态
	- 共有四种状态：
		- committed 提交
		- staged 暂存
		- modified 修改
		- untracked 未追踪的
- ls -a  Linux命令，查看该目录下所有文件名
- git log 查看历史记录
- git config --global core.quotepath false 解决中文乱码
- git add .将目录下的文件添加到暂存区
- git config --global user.name/user.email  配置用户信息 

## 回溯
### Git撤销操作
- git commit --amend 撤销上一次提交，并将暂存区的文件重新提交
- git checkout -- filename  拉取暂存区的文件并将其替换工作区的文件
	- git checkout -- .  撤销文档中修改的所有文件
- git reset HEAD filename  拉去最近一次提交的版本库中的这个文件到暂存区，该操作不影响工作区

### Git版本回退
- git reset --hard HEAD^(回退到上一个版本)
- git reset --hard id（回退到指定id）
	- Tip：
		- git reflog查询每次提交版本id

### Git管理修改
- git之所以被普及，是因为Git跟踪并管理的是修改而非文件
> 当修改同个文件时，第一次修改被add，而后再去进行第二次修改，再commit，这个时候只commit了第一次修改，并非把整个文件commit，而第二次修改还在工作区中。由此可得，git追踪的是修改


### Git撤销修改
- git checkout -- filename
> 当我们在一个文件中不小心写错时，我们可以使用这个命令，将工作区的内容回退到暂存区或者最新版本库。这取决于暂存区中是否有提交该文件
- git reset HEAD filename
>  当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

### 删除文件
- rm filename
 -  删除工作区文件指令
 - 当我们删除工作区文件时，有两种情况：
	 - 确实是要删除文件，那么由于工作区与版本库出现了不同，我们执行以下指令，并commit
		 - git rm filename 
		 - git commit -m'xxx'	
	 - 误删了，执行撤销操作,回退到工作区的版本：
		 - git checkout --filename	


## 远程仓库
- 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
	
		$ ssh-keygen -t rsa -C "youremail@example.com"
- 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”，你就应该看到已经添加的Key

### 添加远程库
- 关联到远程库
		 $  git remote add origin git@github.com:blanche789/git.git
- 将本地库push到远程库
		 $ git push -u origin master
- 以后每次推送只需：
		 $ git push origin master
- Tips：
	- 在github初始创库时，切记要创立一个空库，只要命名即可！

### 从远程库克隆
	$ git clone git@github.com:blanche789/Blog-System.git
- 会自动创建一个名为filename的文件夹，然后将远程库克隆下来

## 分支管理
- 概念：Git可以使同一个项目在同一个时刻，在不同的机器共同开发，并行处理代码，大大缩减了开发进度期


### 创建分支与合并
- 创建分支
	- 代码
			$ git checkout -b branchName 
			==
			$ git branch branchName(创建分支) + $git checkout branchName（跳转到当前分支）
- 合并分支
	- 概念：用于合并指定分支到当前分支
	- 代码：
		 	$ git merge 指定分支
- 查看分支
	- 代码：
		 	$ git branch
	- Tips:
		- 显示时，带有*的分支便为当前分支
- 删除分支：
	- 代码
			$ git branch -d dev

> 工作原理：
>  - 实际上Git的工作过程是跟踪工作内容的修改部分，所以每commit一次，在每个版本里，所记录的为更改的内容，同时定义了master这条指针指向版本库，同时还定义了HEAD指向了master（默认时）。
>  - 当新定义一个分支时，是指向master的，若让新的分支作为当前分支，HEAD会指向当前分支，在当前分支上进行版本更新。
>  - 当跳转回master分支时，工作区的内容会回退到master那个状态。
>  - 当merge时，master与指定分支合并，同时合并两个分支的修改内容，这时候，需要回到工作区判断哪些内容需要留下，进行修改，然后再次在master这条分支上commit，则完成了一次合并

### 解决冲突
> 冲突背景：当master分支与其他分支各提交一次时，由于两个分支都有commit，在合并的时候会产生冲突。这个时候需要人为去解决工作区的冲突，再提交，则合并完成。 
> 合并后的图片如下：
![](https://i.imgur.com/nhpVp3N.png)

### 分支管理策略
> 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

- 代码：
		$ git merge --no-ff -m "merge with no-ff" dev
	- Tips：
		- 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

- 合并后，我们用git log看看分支历史：

		$ git log --graph --pretty=oneline --abbrev-commit
		*   e1e9c68 (HEAD -> master) merge with no-ff
		|\  
		| * f52c633 (dev) add merge
		|/  
		*   cf810e4 conflict fixed
		...
- 分支策略：
	- 在实际开发中，我们应该按照几个基本原则进行分支管理：
	
		- 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	
		- 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	
		- 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
	- 团队合作的分支看起来就像这样
	![](https://i.imgur.com/sAaSmiP.png)

- Tips：
	- 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。


### Bug分支
> 背景：当mater分支上出现一个bug需要及时修复时，我们需要创建一个issue分支出来修复它，可是目前我们dev分支上的工作只进行到一半，无法commit，那么将无法转回master分支，从而创建issue分支。因此，我们通过git stash将工作区的内容存起来

- 代码：
	 	$ git stash

> 当解决完issue分支后，我们转回dev分支，并将stash内容恢复

- 代码：
	 	$ git stash list  //查看stash内容有哪些
		stash@{0}: WIP on dev: f52c633 add merge
		$ git stash pop  //恢复内容到工作区，并将stash内容清楚
- Tips:
	- 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
		- 一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

		- 另一种方式是用git stash pop，恢复的同时把stash内容也删
		- 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
		- 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

### Feature分支
> 背景:在实际开发中，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并。最后，删除该feature分支。该操作是为了避免实验性质的代码（新功能），把主分支搞乱

- 代码：
	  //准备开发
	  $ git checkout -b feature-vulcan

	  //开发完毕
	  $ git add vulcan.py
	  $ git commit -m "add feature vulcan"

	  //准备合并
	  $ git checkout dev

> 有时由于不可抗力因素，在合并前，需要放弃feature已开发的功能。在删除的时候，需要使用-D参数，强行删除
	
	//无效的删除命令
	$ git branch -d feature-vulcan
	error: The branch 'feature-vulcan' is not fully merged.
	If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
	
	//起作用的删除命令
	$ git branch -D feature-vulcan
	Deleted branch feature-vulcan (was 287773e).

### 多人协作
> 一般情况下，在多人合作开发时，我们是在dev分支下进行修改的。若伙伴已经先push他的本地仓库的dev分支到远程仓库的dev。那么我们需要先pull（将伙伴的dev分支信息拉到我们本地dev上），然后再push。但是在pull之前，需要指定本地dev分支与远程origin/dev分支的链接

- 查看远程仓库信息
	- $ git remote
		- 查看远程仓库名称，默认为origin
	- $ git remote -v
		- 显示更详细的信息
		- eg：
				$ git remote -v
			    origin  git@github.com:michaelliao/learngit.git (fetch)
				origin  git@github.com:michaelliao/learngit.git (push)
			
- 推送分支
	- $ git push origin <branch name>
	- Tips:
		- master分支是主分支，因此要时刻与远程同步；
		- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
		- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
		- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
- 抓取分支
> 当我们clone一个项目到本地仓库时，往往只有master分支，创建远程origin的dev分支到本地
- 代码：
	- git checkout -b <branch name> origin/<branch name>
	- Tip:
		- 抓取分支后，就可以时不时向远程仓库push分支

- 推送分支（在他人已经push的情况下）
	- 步骤
		- $ git branch --set-upstream-to=origin/dev dev（先建立连接）
		- $ git pull （将远程dev信息拉取到本地仓库）
		- $ git push origin dev（推送本地dev到远程仓库）

- Tips:

	- 查看远程库信息，使用git remote -v；
	- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
	- 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
	- 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
	- 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
	- 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

### Rebase
> 背景：若将远程库的分支pull下来，那么版本记录会产生交叉分支。如果采用rebase，则可以将历史记录归并成一条线

- 原理：将我们本地仓库的commit挪到了pull下来的commit之后
- $ git rebase
- Tips：
	- rebase操作可以把本地未push的分叉提交历史整理成直线；
	- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。