## Git笔记
- 常用命令
	- git init 初始化仓库
	- git add demo.x 将项目提交到暂存区
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
	- git checkout -- filename  人工撤销文件更改内容
		- git checkout -- .  撤销文档中修改的所有文件

- Git结构：
	- 三层结构：
		- working directory 工作区
		- staging index 暂存区
		- git directory（Repository）版本库

test 十三点asfgasdasd