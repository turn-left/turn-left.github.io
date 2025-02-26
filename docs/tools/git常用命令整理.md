## git常用命令整理

我每天使用 Git ，但是很多命令记不住。

一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。

![img](/docs/tools/img/bg2015120901.png)

下面是我整理的常用 Git 命令清单。几个专用名词的译名如下。

> - Workspace：工作区
> - Index / Stage：暂存区
> - Repository：仓库区（或本地仓库）
> - Remote：远程仓库

### 一、新建代码库

> ```bash
> # 在当前目录新建一个Git代码库
> $ git init
> 
> # 新建一个目录，将其初始化为Git代码库
> $ git init [project-name]
> 
> # 下载一个项目和它的整个代码历史
> $ git clone [url]
> ```

### 二、配置

Git的设置文件为`.gitconfig`，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。

> ```bash
> # 显示当前的Git配置
> $ git config --list
> 
> # 编辑Git配置文件
> $ git config -e [--global]
> 
> # 设置提交代码时的用户信息
> $ git config [--global] user.name "[name]"
> $ git config [--global] user.email "[email address]"
> ```

### 三、增加/删除文件

> ```bash
> # 添加指定文件到暂存区
> $ git add [file1] [file2] ...
> 
> # 添加指定目录到暂存区，包括子目录
> $ git add [dir]
> 
> # 添加当前目录的所有文件到暂存区
> $ git add .
> 
> # 添加每个变化前，都会要求确认
> # 对于同一个文件的多处变化，可以实现分次提交
> $ git add -p
> 
> # 删除工作区文件，并且将这次删除放入暂存区
> $ git rm [file1] [file2] ...
> 
> # 停止追踪指定文件，但该文件会保留在工作区
> $ git rm --cached [file]
> 
> # 改名文件，并且将这个改名放入暂存区
> $ git mv [file-original] [file-renamed]
> ```

### 四、代码提交

> ```bash
> # 提交暂存区到仓库区
> $ git commit -m [message]
> 
> # 提交暂存区的指定文件到仓库区
> $ git commit [file1] [file2] ... -m [message]
> 
> # 提交工作区自上次commit之后的变化，直接到仓库区
> $ git commit -a
> 
> # 提交时显示所有diff信息
> $ git commit -v
> 
> # 使用一次新的commit，替代上一次提交
> # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
> $ git commit --amend -m [message]
> 
> # 重做上一次commit，并包括指定文件的新变化
> $ git commit --amend [file1] [file2] ...
> ```

### 五、分支

> ```bash
> # 列出所有本地分支
> $ git branch
> 
> # 列出所有远程分支
> $ git branch -r
> 
> # 列出所有本地分支和远程分支
> $ git branch -a
> 
> # 新建一个分支，但依然停留在当前分支
> $ git branch [branch-name]
> 
> # 新建一个分支，并切换到该分支
> $ git checkout -b [branch]
> 
> # 新建一个分支，指向指定commit
> $ git branch [branch] [commit]
> 
> # 新建一个分支，与指定的远程分支建立追踪关系
> $ git branch --track [branch] [remote-branch]
> 
> # 切换到指定分支，并更新工作区
> $ git checkout [branch-name]
> 
> # 切换到上一个分支
> $ git checkout -
> 
> # 建立追踪关系，在现有分支与指定的远程分支之间
> $ git branch --set-upstream [branch] [remote-branch]
> 
> # 合并指定分支到当前分支
> $ git merge [branch]
> 
> # 选择一个commit，合并进当前分支
> $ git cherry-pick [commit]
> 
> # 删除分支
> $ git branch -d [branch-name]
> 
> # 删除远程分支
> $ git push origin --delete [branch-name]
> $ git branch -dr [remote/branch]
> ```

### 六、标签

> ```bash
> # 列出所有tag
> $ git tag
> 
> # 新建一个tag在当前commit
> $ git tag [tag]
> 
> # 新建一个tag在指定commit
> $ git tag [tag] [commit]
> 
> # 删除本地tag
> $ git tag -d [tag]
> 
> # 删除远程tag
> $ git push origin :refs/tags/[tagName]
> 
> # 查看tag信息
> $ git show [tag]
> 
> # 提交指定tag
> $ git push [remote] [tag]
> 
> # 提交所有tag
> $ git push [remote] --tags
> 
> # 新建一个分支，指向某个tag
> $ git checkout -b [branch] [tag]
> ```

### 七、查看信息

> ```bash
> # 显示有变更的文件
> $ git status
> 
> # 显示当前分支的版本历史
> $ git log
> 
> # 显示commit历史，以及每次commit发生变更的文件
> $ git log --stat
> 
> # 搜索提交历史，根据关键词
> $ git log -S [keyword]
> 
> # 显示某个commit之后的所有变动，每个commit占据一行
> $ git log [tag] HEAD --pretty=format:%s
> 
> # 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
> $ git log [tag] HEAD --grep feature
> 
> # 显示某个文件的版本历史，包括文件改名
> $ git log --follow [file]
> $ git whatchanged [file]
> 
> # 显示指定文件相关的每一次diff
> $ git log -p [file]
> 
> # 显示过去5次提交
> $ git log -5 --pretty --oneline
> 
> # 显示所有提交过的用户，按提交次数排序
> $ git shortlog -sn
> 
> # 显示指定文件是什么人在什么时间修改过
> $ git blame [file]
> 
> # 显示暂存区和工作区的差异
> $ git diff
> 
> # 显示暂存区和上一个commit的差异
> $ git diff --cached [file]
> 
> # 显示工作区与当前分支最新commit之间的差异
> $ git diff HEAD
> 
> # 显示两次提交之间的差异
> $ git diff [first-branch]...[second-branch]
> 
> # 显示今天你写了多少行代码
> $ git diff --shortstat "@{0 day ago}"
> 
> # 显示某次提交的元数据和内容变化
> $ git show [commit]
> 
> # 显示某次提交发生变化的文件
> $ git show --name-only [commit]
> 
> # 显示某次提交时，某个文件的内容
> $ git show [commit]:[filename]
> 
> # 显示当前分支的最近几次提交
> $ git reflog
> ```

### 八、远程同步

> ```bash
> # 下载远程仓库的所有变动
> $ git fetch [remote]
> 
> # 显示所有远程仓库
> $ git remote -v
> 
> # 显示某个远程仓库的信息
> $ git remote show [remote]
> 
> # 增加一个新的远程仓库，并命名
> $ git remote add [shortname] [url]
> 
> # 取回远程仓库的变化，并与本地分支合并
> $ git pull [remote] [branch]
> 
> # 上传本地指定分支到远程仓库
> $ git push [remote] [branch]
> 
> # 强行推送当前分支到远程仓库，即使有冲突
> $ git push [remote] --force
> 
> # 推送所有分支到远程仓库
> $ git push [remote] --all
> ```

### 九、撤销

> ```bash
> # 恢复暂存区的指定文件到工作区
> $ git checkout [file]
> 
> # 恢复某个commit的指定文件到暂存区和工作区
> $ git checkout [commit] [file]
> 
> # 恢复暂存区的所有文件到工作区
> $ git checkout .
> 
> # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
> $ git reset [file]
> 
> # 重置暂存区与工作区，与上一次commit保持一致
> $ git reset --hard
> 
> # 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
> $ git reset [commit]
> 
> # 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
> $ git reset --hard [commit]
> 
> # 重置当前HEAD为指定commit，但保持暂存区和工作区不变
> $ git reset --keep [commit]
> 
> # 新建一个commit，用来撤销指定commit
> # 后者的所有变化都将被前者抵消，并且应用到当前分支
> $ git revert [commit]
> 
> # 暂时将未提交的变化移除，稍后再移入
> $ git stash
> $ git stash pop
> ```

### 十、其他整理

> ```
> 1) 远程仓库相关命令
> 检出仓库：$ git clone git://github.com/jquery/jquery.git
> 查看远程仓库：$ git remote -v
> 添加远程仓库：$ git remote add [name] [url]
> 删除远程仓库：$ git remote rm [name]
> 修改远程仓库：$ git remote set-url --push [name] [newUrl]
> 拉取远程仓库：$ git pull [remoteName] [localBranchName]
> 推送远程仓库：$ git push [remoteName] [localBranchName]
>  
> *如果想把本地的某个分支test提交到远程仓库，并作为远程仓库的master分支，或者作为另外一个名叫test的分支，如下：
> $git push origin test:master         // 提交本地test分支作为远程的master分支
> $git push origin test:test              // 提交本地test分支作为远程的test分支
>  
> 2）分支(branch)操作相关命令
> 查看本地分支：$ git branch
> 查看远程分支：$ git branch -r
> 创建本地分支：$ git branch [name] ----注意新分支创建后不会自动切换为当前分支
> 切换分支：$ git checkout [name]
> 创建新分支并立即切换到新分支：$ git checkout -b [name]
> 删除分支：$ git branch -d [name] ---- -d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项
> 合并分支：$ git merge [name] ----将名称为[name]的分支与当前分支合并
> 创建远程分支(本地分支push到远程)：$ git push origin [name]
> 删除远程分支：$ git push origin :heads/[name] 或 $ gitpush origin :[name] 
>  
> *创建空的分支：(执行命令之前记得先提交你当前分支的修改，否则会被强制删干净没得后悔)
> $git symbolic-ref HEAD refs/heads/[name]
> $rm .git/index
> $git clean -fdx
>  
> 3）版本(tag)操作相关命令
> 查看版本：$ git tag
> 创建版本：$ git tag [name]
> 删除版本：$ git tag -d [name]
> 查看远程版本：$ git tag -r
> 创建远程版本(本地版本push到远程)：$ git push origin [name]
> 删除远程版本：$ git push origin :refs/tags/[name]
> 合并远程仓库的tag到本地：$ git pull origin --tags
> 上传本地tag到远程仓库：$ git push origin --tags
> 创建带注释的tag：$ git tag -a [name] -m 'yourMessage'
>  
> 4) 子模块(submodule)相关操作命令
> 添加子模块：$ git submodule add [url] [path]
>    如：$git submodule add git://github.com/soberh/ui-libs.git src/main/webapp/ui-libs
> 初始化子模块：$ git submodule init  ----只在首次检出仓库时运行一次就行
> 更新子模块：$ git submodule update ----每次更新或切换分支后都需要运行一下
> 删除子模块：（分4步走哦）
>  1) $ git rm --cached [path]
>  2) 编辑“.gitmodules”文件，将子模块的相关配置节点删除掉
>  3) 编辑“ .git/config”文件，将子模块的相关配置节点删除掉
>  4) 手动删除子模块残留的目录
>  
> 5）忽略一些文件、文件夹不提交
> 在仓库根目录下创建名称为“.gitignore”的文件，写入不需要的文件夹名或文件，每个元素占一行即可，如
> target
> bin
> *.db
>  
> =====================
> Git 常用命令
> git branch 查看本地所有分支
> git status 查看当前状态 
> git commit 提交 
> git branch -a 查看所有的分支
> git branch -r 查看本地所有分支
> git commit -am "init" 提交并且加注释 
> git remote add origin git@192.168.1.119:ndshow
> git push origin master 将文件给推到服务器上 
> git remote show origin 显示远程库origin里的资源 
> git push origin master:develop
> git push origin master:hb-dev 将本地库与服务器上的库进行关联 
> git checkout --track origin/dev 切换到远程dev分支
> git branch -D master develop 删除本地库develop
> git checkout -b dev 建立一个新的本地分支dev
> git merge origin/dev 将分支dev与当前分支进行合并
> git checkout dev 切换到本地dev分支
> git remote show 查看远程库
> git add .
> git rm 文件名(包括路径) 从git中删除指定文件
> git clone git://github.com/schacon/grit.git 从服务器上将代码给拉下来
> git config --list 看所有用户
> git ls-files 看已经被提交的
> git rm [file name] 删除一个文件
> git commit -a 提交当前repos的所有的改变
> git add [file name] 添加一个文件到git index
> git commit -v 当你用－v参数的时候可以看commit的差异
> git commit -m "This is the message describing the commit" 添加commit信息
> git commit -a -a是代表add，把所有的change加到git index里然后再commit
> git commit -a -v 一般提交命令
> git log 看你commit的日志
> git diff 查看尚未暂存的更新
> git rm a.a 移除文件(从暂存区和工作区中删除)
> git rm --cached a.a 移除文件(只从暂存区中删除)
> git commit -m "remove" 移除文件(从Git中删除)
> git rm -f a.a 强行移除修改后文件(从暂存区和工作区中删除)
> git diff --cached 或 $ git diff --staged 查看尚未提交的更新
> git stash push 将文件给push到一个临时空间中
> git stash pop 将文件从临时空间pop下来
> ---------------------------------------------------------
> git remote add origin git@github.com:username/Hello-World.git
> git push origin master 将本地项目给提交到服务器中
> -----------------------------------------------------------
> git pull 本地与服务器端同步
> -----------------------------------------------------------------
> git push (远程仓库名) (分支名) 将本地分支推送到服务器上去。
> git push origin serverfix:awesomebranch
> ------------------------------------------------------------------
> git fetch 相当于是从远程获取最新版本到本地，不会自动merge
> git commit -a -m "log_message" (-a是提交所有改动，-m是加入log信息) 本地修改同步至服务器端 ：
> git branch branch_0.1 master 从主分支master创建branch_0.1分支
> git branch -m branch_0.1 branch_1.0 将branch_0.1重命名为branch_1.0
> git checkout branch_1.0/master 切换到branch_1.0/master分支
> du -hs
> 
> -----------------------------------------------------------
> mkdir WebApp
> cd WebApp
> git init
> touch README
> git add README
> git commit -m 'first commit'
> git remote add origin git@github.com:daixu/WebApp.git
> git push -u origin master
> 
> ```


转自：
- [常用 Git 命令清单](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
- [Git 常用命令大全](https://blog.csdn.net/dengsilinming/article/details/8000622)