Git
===

* 最先进的分布式版本控制系统

  SVN 是集中式版本控制系统，有一个服务器作为大本营，所有的代码都需要提交到服务器上进行统一的管理。当年需要对代码进行改动时，需要先从服务器上下载一份拷贝，修改完之后，还需要上传回服务器。

  在分布式版本控制系统中，大家都拥有一个完整的版本库，不需要联网也可以体交修改，中心服务器不再那么重要。用户可以把各自的修改推送给对方。

* 初次使用 Git 前的配置

  - 设置用户信息，以后每一个 Git 的提交都会使用这些信息，**一旦确定不可更改**。

    ```bash
    git config --global user.name "usename"
    git config --global user.email "youremail"
    git config --list #查看信息是否写入成功。
    ```

* git 中文乱码解决

  ```bash
   git config --global core.quotepath false
  ```

# Git常用命令速查手册

![96](https://upload.jianshu.io/users/upload_avatars/1153338/d63d8b3f-1d39-459a-a808-64ef752a80c1.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)

 

[大老哈](https://www.jianshu.com/u/c10fd5e3fcbb)

 

关注

2018.12.12 13:32 字数 1488 阅读 228评论 0喜欢 16

1. 初始化仓库

- git init

1. 将文件添加到仓库

- git add 文件名 # 将工作区的某个文件添加到暂存区
- git add -u # 添加所有被tracked文件中被修改或删除的文件信息到暂存区，不处理untracked的文件
- git add -A # 添加所有被tracked文件中被修改或删除的文件信息到暂存区，包括untracked的文件
- git add . # 将当前工作区的所有文件都加入暂存区
- git add -i # 进入交互界面模式，按需添加文件到缓存区

1. 将暂存区文件提交到本地仓库

- git commit -m "提交说明" # 将暂存区内容提交到本地仓库
- git commit -a -m "提交说明" # 跳过缓存区操作，直接把工作区内容提交到本地仓库

1. 查看仓库当前状态

- git status

1. 比较文件异同

- git diff # 工作区与暂存区的差异
- git diff 分支名 #工作区与某分支的差异，远程分支这样写：remotes/origin/分支名
- git diff HEAD # 工作区与HEAD指针指向的内容差异
- git diff 提交id 文件路径 # 工作区某文件当前版本与历史版本的差异
- git diff --stage # 工作区文件与上次提交的差异(1.6 版本前用 --cached)
- git diff 版本TAG # 查看从某个版本后都改动内容
- git diff 分支A 分支B # 比较从分支A和分支B的差异(也支持比较两个TAG)
- git diff 分支A...分支B # 比较两分支在分开后各自的改动
  `另外：如果只想统计哪些文件被改动，多少行被改动，可以添加 --stat 参数`

1. 查看历史记录

- git log # 查看所有commit记录(SHA-A校验和，作者名称，邮箱，提交时间，提交说明)
- git log -p -次数 # 查看最近多少次的提交记录
- git log --stat # 简略显示每次提交的内容更改
- git log --name-only # 仅显示已修改的文件清单
- git log --name-status # 显示新增，修改，删除的文件清单
- git log --oneline # 让提交记录以精简的一行输出
- git log –graph –all --online # 图形展示分支的合并历史
- git log --author=作者 # 查询作者的提交记录(和grep同时使用要加一个--all--match参数)
- git log --grep=过滤信息 # 列出提交信息中包含过滤信息的提交记录
- git log -S查询内容 # 和--grep类似，S和查询内容间没有空格
- git log fileName # 查看某文件的修改记录，找背锅专用

1. 代码回滚

- git reset HEAD^ # 恢复成上次提交的版本
- git reset HEAD^^ # 恢复成上上次提交的版本，就是多个^，以此类推或用~次数
- git reflog
- git reset --hard 版本号
- --soft：只是改变HEAD指针指向，缓存区和工作区不变；
- --mixed：修改HEAD指针指向，暂存区内容丢失，工作区不变；
- --hard：修改HEAD指针指向，暂存区内容丢失，工作区恢复以前状态；

1. 同步远程仓库

- git push -u origin master

1. 删除版本库文件

- git rm 文件名

1. 版本库里的版本替换工作区的版本

- git checkout -- test.txt

1. 本地仓库内容推送到远程仓库

- git remote add origin [git@github.com](mailto:git@github.com):帐号名/仓库名.git

1. 从远程仓库克隆项目到本地

- git clone [git@github.com](mailto:git@github.com):git帐号名/仓库名.git

1. 创建分支

- git checkout -b dev
  `-b表示创建并切换分支`
  上面一条命令相当于一面的二条：
- git branch dev //创建分支
- git checkout dev //切换分支

1. 查看分支

- git branch

1. 合并分支

- git merge dev
  `用于合并指定分支到当前分支`
- git merge --no-ff -m "merge with no-ff" dev
  `加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并`

1. 删除分支

- git branch -d dev

1. 查看分支合并图

- git log --graph --pretty=oneline --abbrev-commit

1. 查看远程库信息

- git remote
  `-v 显示更详细的信息`

1. git相关配置
   `安装完Git后第一件要做的事，设置用户信息(global可换成local在单独项目生效)`

- git config --global user.name "用户名" # 设置用户名
- git config --global user.email "用户邮箱" #设置邮箱
- git config --global user.name # 查看用户名是否配置成功
- git config --global user.email # 查看邮箱是否配置
- git config --global --list # 查看全局设置相关参数列表
- git config --local --list # 查看本地设置相关参数列表
- git config --system --list # 查看系统配置参数列表
- git config --list # 查看所有Git的配置(全局+本地+系统)
- git config --global color.ui true //显示git相关颜色

1. 撤消某次提交

- git revert HEAD # 撤销最近的一个提交
- git revert 版本号 # 撤销某次commit

1. 拉取远程分支到本地仓库

- git checkout -b 本地分支 远程分支 # 会在本地新建分支，并自动切换到该分支
- git fetch origin 远程分支:本地分支 # 会在本地新建分支，但不会自动切换，还需checkout
- git branch --set-upstream 本地分支 远程分支 # 建立本地分支与远程分支的链接

1. 标签命令

- git tag 标签 #打标签命令，默认为HEAD
- git tag #显示所有标签
- git tag 标签版本号 #给某个commit版本添加标签
- git show 标签 #显示某个标签的详细信息

1. 同步远程仓库更新

- git fetch origin master
  `从远程获取最新的到本地，首先从远程的origin的master主分支下载最新的版本到origin/master分支上，然后比较本地的master分支和origin/master分支的差别，最后进行合并`
  git fetch比git pull更加安全