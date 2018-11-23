# Git学习文档
***
## 一、概念
***
### （一）、Git是什么
Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

Git不但能自动记录每次文件的改动，还可以让他人协作编辑，这样就不用自己管理一堆文件，也不需要把文件传来传去。

有GitHub、码云等为开源项目免费提供Git储存
***
### （二）、Git与SVN的区别
Git与SVN均为版本控制系统，它们的区别如下：

1. Git是分布式的，SVN不是：这是Git和其它非分布式的版本控制系统，例如SVN，CVS等，最核心的区别。

2. Git把内容按元数据方式存储，而SVN是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn，.cvs等的文件夹里。

3. Git分支和SVN的分支不同：分支在SVN中一点不特别，就是版本库中的另外的一个目录。

4. Git没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比Git缺少的最大的一个特征。

5. Git的内容完整性要优于SVN：Git的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。

[SVN简介](http://www.runoob.com/svn/svn-intro.html)
***
### （三）、工作区与暂存区
工作区：在电脑里能看到的目录

暂存区：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

版本库:工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系：
![Working Directory](http://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)

[详细情况查看这个链接](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013745374151782eb658c5a5ca454eaa451661275886c6000)
***
## 二、Git常用命令
***

###Git安装相关

#### （一）、移除旧版本git
```
[root@Git ~]# git --version
git version 1.8.3.1
```    
【说明】查看自带的版本
```
[root@Git ~]# yum remove git   
```
【说明】移除原来的版本

#### （二）、 安装所需软件包
```
[root@Git ~]# yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
[root@Git ~]# yum install gcc-c++ perl-ExtUtils-MakeMaker
```
#### （三）、下载&安装
```
[root@Git ~]# cd /usr/src
[root@Git ~]# wget https://www.kernel.org/pub/software/scm/git/git-2.7.3.tar.gz
```
#### （四）、 解压
```
[root@Git ~]# tar xf git-2.7.3.tar.gz
```
#### （五）、 配置编译安装
```
[root@Git ~]# cd git-2.7.3
[root@Git ~]# make configure
[root@Git ~]# ./configure --prefix=/usr/git ##配置目录
[root@Git ~]# make profix=/usr/git
[root@Git ~]# make install
```
#### （六）、 加入环境变量path
```
[root@Git ~]# echo "export PATH=$PATH:/usr/git/bin" >> /etc/profile
[root@Git ~]# source /etc/profile
```
#### （七）、 检查版本version
```
[root@Git git-2.7.3]# git --version
git version 2.7.3
```
***
###Git基本操作
#### （一）、配置用户名和电子邮件地址
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
【说明】Git安装完成后，需要配置用户信息：用户名和电子邮件地址。这两条配置很重要，每次Git提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录。
#### （二）、CREATE 创建
##### 1、克隆已存在的仓库
```
$ git clone ssh://user@domain.com/repo.git
```
【说明】命令 ```git clone```后面跟的是GitLab中项目的SSH地址。若未设置SSH Key，则需要设置，具体方法请戳[Git生产ssh秘钥](https://blog.csdn.net/zhangming1013/article/details/78928340)
##### 2、创建一个新的仓库
```
$ git init
```
【说明】例如，在E盘新建一个文件夹test作为**仓库**，进入该文件夹，右键选择“Git Bash Here”，输入命令```git init```，提示“Initialized empty Git repository in E:/test/.git”，则创建成功。
#### （三）、LOCAL CHANGES 本地修改
##### 1、查看仓库当前状态
```
$ git status
```
【说明】例如，在上述Git Bash状态，输入命令```git status```，则会显示当前仓库状态信息，若增加或修改了文件，则会显示相应的操作及操作内容。
##### 2、添加文件
```
$ git add FileName.suffix
```
【说明】例如，在上诉Bash状态，输入命令```vi readme.txt```创建并编辑readme.txt文件，输入```i```进入编辑模式，码内容，码完后按Esc键退出编辑模式，输入```:wq```并回车保存文件，此时文件创建完毕。输入命令```git add readme.txt```。若出现警告“warning: LF will be replaced by CRLF in readme.txt”，[请参考该文档](https://blog.csdn.net/MissPuff07/article/details/83548847)。
##### 3、提交之前完成的修改
```
$ git commit -m <message>
```
【说明】例如，在上诉状态下，输入命令```git commit -m "wrote a readme file"```，提交到仓库。```-m```后面输入的是本次提交的说明，内容最好具有意义，方便查看。若只输入```git commit```，不输入```-m```以及后面的信息，则会进入vim模式。

【说明2】可一次提交多个文件，例如：
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```
##### 4、查看修改内容
```
$ git diff
```
【说明】```git diff```顾名思义就是查看difference，显示的格式是Unix通用的diff格式。若修改文件后使用该命令，则会显示具体修改的详情。修改内容后，输入```git add ChangedFileName.suffix```进行存储，输入```git commit -m "message"```进行提交。
#### （四）、COMMIT HISTORY 提交历史
##### 1、显示所有的提交记录
```
$ git log
```
【说明】显示所有的提交操作，从最新的提交开始显示。
##### 2、显示指定文件的修改信息
```
$ git log -p <FileName>
```
##### 3、显示指定文件的修改记录（修改时间和修改位置）
```
$ git blame <FileName.suffix>
```
#### （五）、BRANCHES & TAGS 分支和标签
##### 1、显示所有已存在的分支
```
$ git branch -av
```
##### 2、切换HEAD分支或指定分支
```
$ git checkout <BranchName>
```
【说明】命令```git checkout```为切换到HEAD分支，若后面加上BranchName，则会切换到指定的分支。
##### 3、在当前HEAD基础上新建一个分支
```
$ git branch <NewBranchName>
```
##### 4、基于远程分支创建一个新的跟踪分支
```
$ git checkout --track <RemoteName/BranchName>
```
##### 5、删除本地分支
```
$ git branch -d <BranchName>
```
##### 6、删除远程分支
```
$ git branch -d -r <BranchName>
```
##### 7、使用标签标记当前提交
```
$ git tag <TagName>
```
##### 8、创建并切换分支
```
$ git checkout -b <BranchName>
```
【说明】该命令等于以下两条命令：
```
$ git branch <TheBranchName>
$ git checkout <TheBranchName>
```
##### 9、查看当前分支
```
$ git branch
```
***
#### （六）、UPDATE & PUBLISH 更新和发布

##### 1、列出当前所有的一配置的远程仓库
```
$ git remote -v
```
##### 2、关联远程仓库
```
$ git remote add <RemoteName> <url>
```
##### 3、显示指定远程仓库的信息
```
$ git remote show <RemoteName>
```
##### 4、直接下载更改并合并到HEAD中
```
$ git pull <RemoteName> <branch>
```
##### 5、从远程仓库下载更新，但不合并到HEAD中
```
$ git fetch <RemoteName>
```
##### 6、将本地更改发布到远程仓库中
```
$ git push <RemoteName> <branch>
```
【说明】有可能会发布失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用```git pull```把最新的提交从origin抓下来并在本地合并，解决冲突，再发布。[参考链接](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013760174128707b935b0be6fc4fc6ace66c4f15618f8d000)
##### 7、删除远程上的分支
```
$ git branch -dr <RemoteName/BranchName>
```
##### 8、发布标签
```
$ git push --tags
```
***
#### （七）、MERGE & REBASE 合并和变基
##### 1、删除文件
```
$ git rm FileName.suffix
```
【说明】删除该文件后，可使用命令```git reset --hard HEAD```进行文件恢复，也可通过```git reset --hard <commit_id> ```恢复指定内容。
##### 2、合并分支到当期的HEAD
```
$ git merge <BranchName>
```
##### 3、变基
```
$ git rebase
```
【说明】[详情请戳链接](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0015266568413773c73cdc8b4ab4f9aa9be10ef3078be3f000)
***
#### （八）、UNDO 撤销
##### 1、放弃工作中的所有本地更改
```
$ git reset --hard HEAD
```
【说明】HEAD为当前版本，若修改txt文件并add，但未commit，则HEAD指向为修改之前的版本（即上一个版本），若commit后，则指向当前的修改后的版本。
##### 2、返回到指定版本
```
$ git reset --hard <commit_id>
```
【说明】使用```git log```命令，会显示commit、Author、Date和commit message信息，commit后面的字符标识即为此命令中的```<commit_id>```，可只输入前几位。eg:```git reset --hard b3634```。使用命令```git reflog```可查看所有的命令。
***
### 三、相关链接

1. [Git官网](https://git-scm.com/ "Git官网")

2. [Git菜鸟教程](http://www.runoob.com/git/git-tutorial.html "Git菜鸟教程")

3. [Git易懂教程（廖雪峰的官方网站）](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/ "Git易懂教程")
4. [最新git源码下载地址1](https://www.kernel.org/pub/software/scm/git/)
5. [最新git源码下载地址2](https://github.com/git/git/releases)

【说明】可以手动下载下来在上传到服务器上面
