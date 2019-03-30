## Git笔记
- 常用命令
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

### Git结构：
- 三层结构：
	- working directory 工作区
	- staging index 暂存区
	- git directory（Repository）版本库

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


### 远程仓库
- 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
	
		$ ssh-keygen -t rsa -C "youremail@example.com"
- 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”，你就应该看到已经添加的Key

git remote add origin https://github.com/blanche789/git.git
git push -u origin master