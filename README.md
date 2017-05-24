
## 第一章 初次运行git的配置
### 1. 设置用户名和用户邮箱  
```  
~$ git config --global user.name "John"
~$ git config --global user.email "John@163.com"
```  
***若要给指定的项目使用其他的邮箱和用户名，可以去掉global参数***    
### 2. 查看所有配置信息    
```
~$ git config --list
```    
### 3. 查看指定的信息
#### 3.1 查看用户名  
```  
~$ git config user.name
```  
#### 3.2 查看用户邮箱  
```  
~$ git config user.email
```    
### 4. 设置git默认打开的编辑工具
```
~$ git config --global core.editor
```
### 5. 获取帮助
```
~$ git help <verb>
~$ git <verb> --help
~$ man git-<verb>
```    
如：  
```
~$ git help config
~$ git config --help
~$ man git-config
```  



## 第二章 git基本操作
### 1. 创建仓库
- 方式一：在已存在的目录下创建仓库  
```
$ git init
```
- 方式二：从服务器上克隆仓库到本地  
```
git clone url [repository_name]
```
    - url表示的是远程仓库的名字
    - repository_name是你本地仓库的名字，可以不指定
      
### 2. 跟踪文件
- 工作区中文件的状态有两种
    - 已跟踪：在仓库已经存在该文件的快照，工作一段时间后，被跟踪的文件的状态有以下三种情况
         - 未修改
         - 已修改
         - 已暂存 
    - 未跟踪：仓库中不存在文件的快照，而且不在暂存区中，一般新创建的文件属于未跟踪状态
- 查看文件详细状态信息   
```
$ git status
```  
    - 未跟踪文件：提示`Untracked files`
    - 未跟踪的文件被放入暂存区：提示`Changes to be committed`
    - 已跟踪的文件被修改但是没有放入暂存区：提示`Changes not staged for commit`

- 查看文件简略状态信息
```
$ git status -s
```
    - A表示新增加到暂存区的文件所处的状态
    - D表示文件处于被删除状态
    - ??表示文件处于未跟踪状态
    - &nbsp;M表示文件被修改但是没有放入暂存区的状态
    - M&nbsp;表示文件被修改且而且被暂存到暂存区但是未被提交的状态
    - MM表示文件被修改并放入暂存区，之后又修改了文件 
 
- 将指定文件放入暂存区
```
$ git add (files)
```
- 将工作区中所有文件放入暂存区中  
```
$ git add .
```

### 3. 忽略文件    
- 编写.gitignore文件  
- 所有空行或者以#开头的行都会被 Git 忽略。  
- 编写规范：  
	- 可以使用标准的 glob 模式匹配
	- 匹配模式可以以(/)开头防止递归
	- 匹配模式可以以(/)结尾指定目录
	- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号(!)取反
	- 星号(*)匹配零个或多个任意字符
	- [abc] 匹配任何一个列在方括号中的字符(这个例子要么匹配一个a，要么匹配一个b，要么匹配一个c)
	- 问号(?)只匹配一个任意字符
	- 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配(比如[0-9]表示匹配所有 0 到 9 的数字)
	- 使用两个星号表示匹配任意中间目录，比如a/**/z可以匹配a/z，a/b/z或a/b/c/z等

### 4. 比较版本区别
- 关于diff的格式
	- diff命令： `$ diff <变动前的文件> <变动后的文件>` 
	- 始终记住：diff命令显示的结果是**变动前的文件需要经过怎样的变换才能与变动后的文件完全一致**
	- 参看文章[diff详解,读懂diff结果阅读目录](http://www.cnblogs.com/wangqiguo/p/5793448.html)
	- 参看文章[读懂diff](http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html)
- 比较工作目录中当前文件与暂存区快照之间的区别，也就是修改了但是没有暂存起来的内容。此时变动前的文件指的是已暂存的文件，变动后的文件指的是工作区中被修改的同名文件------暂存区的文件要经过怎样的变换与工作区被修改的文件完全一致
```
$ git diff
```
- 查看已暂存的将要添加到下次提交里的内容。此时变动前的文件指的是在仓库中的文件，变动后的文件指的是暂存区同名的文件-------仓库中的文件要经过怎样的变换才能与暂存区中同名文件内容完全一致
```
$ git diff --staged
或者
$ git diff --cached
```

### 5. 提交
- 将暂存区中的快照提交到仓库中
- 每次提交都是做一次快照
- 使用默认编辑器编辑commit信息
```
$ git commit
```
- 提交的同时输入commit信息
```
$ git commit -m commitMessage
```
- 跳过暂存区直接将**已被跟踪**的文件的**修改**提交
```
$ git commit -a -m commitMessage
```

### 6. 删除文件
- 被删除的文件不再被跟踪，在工作区的相应文件也被删除
- 注意删除操作删除的是暂存区的文件
- 删除被跟踪但删除之前未被修改的文件
```
$ git rm filename
```
- 若只是简单的使用rm命令删除工作区被跟踪的文件，使用git status将提示"Changes not staged for commit"
- 删除被修改且已经被暂存到暂存区的文件
```
$ git rm -f filename
```
- 删除被跟踪的文件，但在工作区中保留该文件
```
$ git rm --cache filename
```
- 删除目录中的文件
```
$ git rm dirName/fileName
```
	- 可以使用glob模式----如：删除temp目录中以~结尾的文件，注意星号要转义，即在其之前使用反斜杠
	```
		git rm temp/\*~
	```

### 7. 重命名文件
```
$ git mv file_from file_to
```

### 8. 查看提交历史
- 使用`git log`命令
- git log的常用选项
	- 限制git log输出的格式
		- -p 按补丁格式显示每个更新之间的区别
		- --stat 显示每次更新的文件的修改统计信息
		- --shortstat 只显示--stat中最后的行数修改添加的统计
		- --name-only 仅在提交信息后显示已修改的文件的清单
		- --name-status 显示新增、修改、删除文件的清单
		- --abbrev-commit 仅显示哈希值的前几个字符，而非所有40个字符
		- --relative-date 使用较短的相对时间显示
		- --graph 显示ASCII图形表示的分支合并历史
		- --pretty 使用其他格式显示历史提交信息。可用的选项包括oneline，short，full，fuller 和format（后跟指定格式）
			- `git log --pretty=format`的常用子选项如下所示：
				- %H 提交对象的完整哈希字串
				- %h 提交对象的简短哈希字串
				- %T 树对象的完整哈希字串
				- %t 树对象的简短哈希字串
				- %P 父对象的完整哈希字串
				- %p 父对象的简短哈希字串
				- %an 作者的名字
				- %ae 作者的电子邮箱地址
				- %ad 作者修改日期（可以使用--date==选项来定制格式）
				- %ar 作者修改日期，按多久以前的方式显示
				- %cn 提交者的名字
				- %ce 提交者的电子邮件地址
				- %cd 提交的日期
				- %cr 提交日期，按多久以前的方式显示
				- %s 提交说明 
				- 例子：` $ git log --pretty=format:"%h %an %ae %ad %s"`
				- 注意：作者指的是实际上做出修改的人，提交者指的是最后将该工作提交到仓库的人。当我们给项目提交补丁的时候就可能出现这种情况，你将你的补丁发给项目的某个核心成员，该核心成员将补丁合并到项目中，此时你就是作者，而项目负责人就是提交者
	- 限制git log的输出条件
		- -(n) 仅显示最近的n条提交，n为整数
		- --since，--after 仅显示指定时间之后的提交。如：显示十分钟前提交的历史，`$ git log --since=10.minutes`，这里注意到10与minute之间有一个点号；显示时间2008年10月1号之后提交的历史`git log --since="2008-10-1"`
		- --util，--before 仅显示指定时间之前的提交
		- --author 仅显示指定作者的相关提交
		- --committer 仅显示指定提交者相关的提交
		- --grep 仅显示含指定关键字的提交
		- -S 仅显示添加或移除了某一个关键字的提交，如`git log -Sfunction_name`可以用来找出添加或者移除某一个特定函数的提交，其中function_name指的是函数名
 
### 9. 撤销操作
#### 9.1 撤销提交
- 修改最后一次提交
	- 使用命令`git commit --amend`
	- 若自上次提交没有再做任何的修改，如提交后立即使用使用上述的命令，此时不改变已提交快照的内容，只改变提交信息
	- 若提交后才发现自己少提交了某些文件，此时我们可以先将还要提交的文件暂存到暂存区，然后执行上述的命令重新提交，最终你只会有一个提交，第二次的提交将覆盖第一次的提交，如
	```
		$ git add 3
		$ git commit -m 'commit file 3'
		$ git add 4
		$ git commit --amend
	```  

### 9.2 取消暂存
- 使用命令`git reset HEAD <file>`
	- 不暂存指定的文件
	- 只修改暂存区
	- 不会影响工作区 
- 使用命令`git reset --hard`
	- **危险命令**
	- 可能会丢失工作区的进度

### 9.3 撤销工作区的修改
- 使用命令`git checkout -- [file]`
	- **危险命令**
	- **不可逆**
	- 将工作区中被跟踪的文件还原到上一次提交的状态
	- 实质上是拷贝仓库中的文件覆盖工作区的文件 

### 10. 远程仓库管理
#### 10.1 查看远程仓库
- 使用命令`git remote`
	- 列出每一个远程仓库的简写
	- 若使用`git clone`克隆仓库默认会列出一个叫做origin的项
- 使用命令`git remote -v`
	- 列出每一个远程仓库的简写及对应的fetch，push的URL地址  

#### 10.2 添加远程仓库
- 使用命令`git remote add <shortname> <url>`
	- shortname表示的是远程仓库的简写
	- url表示的是远程仓库的地址

#### 10.3 从远程仓库中抓取数据
- 抓取下来的数据是远程仓库有但是本地仓库没有的
- 使用命令`git fetch [remote-name]`
	- 将远程仓库中的所有分支都拉取到本地中
	- 不自动合并到当前分支
	- 可以随时进行合并和查看
		- 查看远程分支命令：`$ git branch -r`  
  		- 切换到远程分支命令：`$ git checkout remote-name/remote-branch-name`，如`$ git checkout origin/master`查看远程orgin的master分支
  		- 删除远程分支命令：`$ git branch -r -d remote-name/remote-branch-name`，如`$ git branch -r -d origin/master`
- 使用命令`git pull`
	- 前提：本地分支被设置为跟踪远程分支
	- 命令尝试将从远程仓库中拉取下来的更新合并到本地仓库中 
	- `git clone`命令会自动设置本地master分支跟踪克隆的远程仓库的master分支

#### 10.4 推送到远程仓库中
- 使用命令`git push [remote-name] [branchname]`
- 命令将本地当前分支的更新推送到远程仓库指定的分支上
- 当远程仓库发生变化时（如你的合作伙伴在你推送之前先将自己的更新推送到了远程仓库中），必须先将远程仓库的更新拉下来并且合并到当前分支上，然后重新推送到远程分支上

#### 10.5 查看远程仓库
- 使用命令`git remote show [remote-name]`查看指定的远程仓库
- 显示结果解释：
 
```
1	* remote origin
2 	URL: https://github.com/my-org/complex-project
3 	Fetch URL: https://github.com/my-org/complex-project
4 	Push URL: https://github.com/my-org/complex-project

5 	HEAD branch: master

6 	Remote branches:
7 		master tracked
8 		dev-branch tracked
9 		markdown-strip tracked
10		issue-43 new (next fetch will store in remotes/origin)
11 		issue-45 new (next fetch will store in remotes/origin)
12 		refs/remotes/origin/issue-11 stale (use 'git remote prune' to remove)
 	
13	Local branches configured for 'git pull':
14 		dev-branch merges with remote dev-branch
15 		master merges with remote master

16 	Local refs configured for 'git push':
17 		dev-branch pushes to dev-branch (up to date)
18 		markdown-strip pushes to markdown-strip (up to date)
19 		master pushes to master (up to date)
```
- 第1-4行：origin的URL地址；fetch与push的URL地址
- 第5行：origin默认分支的名字，一般是master分支
- 第6-12行：关于远程分支的描述
	- tracked：表示该分支已被跟踪
	- new：表示该分支值存在远程仓库中
	- stale：表示该分支在远程仓库中已被删除
- 第13-15行：表示本地分支**默认**合并的远程分支
- 第16-19行：表示本地分支**默认**推送到的远程分支
	- up to date：表示本地分支与远程分支同步
	- fast-forwardable： 表示本地分支超前于远程分支
	- local out of date： 表示本地分支落后与远程分支

#### 10.6 远程仓库的移除与重命名
- 重命名远程仓库简名
	- 使用命令`git remote rename old_name new_name` 
	- 如以代码`$ git remote rename origin test`将origin简名改为了test
- 移除远程仓库
	- 使用命令`git remote rm [remote_name]`
	- 移除远程仓库的情况：
		- 你已经从服务器上搬走
		- 不再使用某一特定的镜像
		- 某一贡献者不再贡献
	- 注意：**使用该命令移除的是对远程仓库的引用，而不是真的在服务器上移除该仓库，实际上该远程仓库在服务器上还是存在的** 

### 11. 打标签
#### 11.1 简述
- 给某一提交打上标签，以示重要
- 便于查找
- 标记发布点，即版本

#### 11.2 列出标签
- 使用命令`git tag`列出所有的标签
- 使用命令`git tag -l pattern`列出符合pattern的标签，如`git tag -l 'v1.8.5*'`列出了1.8.5系列的标签

#### 11.3 标签的种类
- 轻量标签（lightweight）
	- 表示对特定提交的引用 
- 附注标签（annotated）
	- 一个完整对象
	- 可以被校验
	- 包括打标签人的名字，邮箱，日期时间，标志信息等

#### 11.4 创建附注标签
- 使用命令`git tag -a tag_name -m tag_info`，如`git tag -a v1.4 -m 'my version 1.4'`

#### 11.5 创建轻量标签
- 使用命令`git tag tag_name`

#### 11.6 显示标签信息
- 使用命令`git show`将显示所有的标签信息
- 使用命令`git shwo tag_name`将显示名为tag_name的标签信息

#### 11.7 后期打标签
- 上面创建标签的方法都是针对最后一次提交的，使用命令`git tag -a tag_name hash_code`可以给过去的提交打标签，如`git tag -a v1.2 9fceb02`

#### 11.8 共享标签
- 默认情况下，git push并不会将标签推到远程仓库上，必须显式地将标签推到远程仓库上
- 使用命令`git push [origin_name] [tag_name]`将名为tag_name的标签推到名为origin_name的远程仓库中
- 添加--tags选项可以一次性将所有不在远程仓库的标签推到服务器那里，如`git push origin --tags`将所有不在origin的标签推送到origin所在的服务器那里

#### 11.9 检出标签
- 使用命令`git checkout -b [branchname] [tagname]`

### 12. 别名
- 执行命令`git config --global alias.ci commit `后，执行`git ci`相当于执行`git commit`
- 执行命令`git config --global alias.br branch`后，执行`git br`相当于执行`git branch`
- 执行命令`git config --global alias.unstage 'reset HEAD --'`，执行`git unstage fileA`相当于执行`git reset HEAD -- fileA`
- 可以使用类似于上面的做法给其他的命令起别名


