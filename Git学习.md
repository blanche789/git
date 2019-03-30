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
>  