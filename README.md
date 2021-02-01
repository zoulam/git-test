* [推荐文章](#推荐文章)
* [什么是git](#什么是git)
* [在此之前](#在此之前)
* [git使用（入门）](#git使用入门)
  * [①初始化本地配置](#初始化本地配置)
  * [②通过 <a href="https://github\.com">github</a>初始仓库](#通过-github初始仓库)
    * [方式1（推荐使用）](#方式1推荐使用)
    * [方式2](#方式2)
* [什么是GitHub](#什么是github)
* [概念初识](#概念初识)
  * [①文件的几个概念](#文件的几个概念)
  * [②reflog](#reflog)
  * [③branch&amp;tag](#branchtag)
* [<strong>常见命令</strong>](#常见命令)
  * [建议](#建议)
  * [常见参数](#常见参数)
  * [help](#help)
  * [add](#add)
  * [commit](#commit)
    * [值得一提](#值得一提)
    * [概念理解](#概念理解)
  * [clone](#clone)
  * [<strong>pull&amp;push</strong>](#pullpush)
    * [出现冲突](#出现冲突)
      * [方式1](#方式1)
      * [方式2](#方式2-1)
      * [方式3](#方式3)
  * [config](#config)
  * [checkout（查看源码的神器）](#checkout查看源码的神器)
  * [<strong>status</strong>](#status)
  * [diff](#diff)
  * [mv &amp; rm](#mv--rm)
  * [merge](#merge)
  * [log&amp;reflog](#logreflog)
    * [log可选参数](#log可选参数)
  * [<strong>remote</strong>](#remote)
* [变基（rebase）](#变基rebase)
    * [1、branch](#1branch)
    * [2、pull rebase](#2pull-rebase)
    * [2、merge commit message](#2merge-commit-message)
      * [方法1](#方法1)
      * [方法2](#方法2)
      * [其他](#其他)
* [常见操作](#常见操作)
  * [amend（本地）](#amend本地)
* [撤销三连](#撤销三连)
  * [undo&amp;redo(本地)](#undoredo本地)
  * [revert](#revert)
  * [reset（本地）](#reset本地)
* [暂存内容](#暂存内容)
  * [stash](#stash)
* [可视化工具](#可视化工具)
* [常见问题](#常见问题)
  * [1）需要每一次的git push都需要输入账号密码](#1需要每一次的git-push都需要输入账号密码)
  * [2）release|merge进程未中断](#2releasemerge进程未中断)
  * [3）git push出现rejected错误](#3git-push出现rejected错误)
  * [4）关于中文乱码问题](#4关于中文乱码问题)
  * [5）ls打印中文目录是乱码](#5ls打印中文目录是乱码)
  * [6）如何生成在GitHub可以使用的目录](#6如何生成在github可以使用的目录)
  * [7）如何更新git客户端](#7如何更新git客户端)
  * [8）Submodule 和 Subtree区别和使用](#8submodule-和-subtree区别和使用)

# 推荐文章

[git进阶指南](https://gb.yekai.net/)

# 什么是git

git是一个分布式版本控制（ **distributed version-control**）系统。

​	通常会被缩写成 `VSC` ： **version control system**

​	常用大型软件系统的开发，利于协作。

更多git信息：[git的wiki](https://zh.wikipedia.org/wiki/Git)  [git官方文档](https://git-scm.com/doc)

# 在此之前

> 1、 注册[GitHub](http://github.com/)账号
>
> 2、安装[git客户端](https://git-scm.com/)，并更新到最新版本

# git使用（入门）

## ①初始化本地配置
1、设置本地邮箱和账户名字(如果是你自己的电脑可以写入参数 `--gobal`)
```bash {.line-numbers}
git config user.name "<username>"
git config user.email "<email>"
```

2、生成ssh(sshkey生成器是git客户端自带的)

>  生成的key会在ssh传输中进行校验，同时可以确保你拥有自主 `push`远程仓库的权限。

①`in bash terminal`

```bash {.line-numbers}
ssh-keygen -t rsa -C "<your eamil>"#这个步骤生成的sshkey路径会显示在终端，注意查看

# example
ssh-keygen -t rsa -C "zoulam19981205@163.com"
```

②将生成的sshkey粘贴到GitHub账户上（**此步是保证你的电脑自由使用ssh对该账户的仓库操作**）

`setting` -> `SSH GPG keys` -> `new SSH key`-> 粘贴上一步保存的sshkey并填写key名称


## ②通过 [github](https://github.com)初始仓库
### 方式1（推荐使用）

1、在GitHub上点击 `New repository` (choose `REAMDE.md`、`LICENSE`、`.gitignore`)

[.gitignore template](https://github.com/github/gitignore)

2、克隆上一步创建的远程仓库 `git clone url`

### 方式2

>  ​	需要**注意**的是：在 `2020/10/1`之后创建的GitHub仓库默认分支是 `main`而不是过去的 `master`。
>
> ​	当然你也可以自定义默认分支（指在GitHub网站上操作）： `setting` -> `Repositories` -> `Repository default branch`填入 你想要的默认创建分支名，然后 `update`

```bash
git init # 初始化git项目

# 如果安装的是新版git客户端且自定义分支名就是main则省略这一步
git checkout -b main #创建main分支并切换到main分支
git add README.md # 将README.md 文件创建并移交暂存区
git commit -m "first commit"# 发起commit，m是message，message内容是first commit
git branch -M main
git remote add origin <url>
git push -u origin main #
```

# 什么是GitHub

>  GitHub提供免费的私有仓库托管服务，是世界上毫无争议被认为是**最好**开源网站，在2018年6月份被微软收购，题外话就是：npm也被微软收购 [参见营销号量子位的文章](https://www.qbitai.com/2020/03/12395.html)

[github中文文档](https://docs.github.com/cn) ：里面包含大量的GitHub知识。比起所谓的垃圾博客好一万倍，建议选择英文查看（当然中文文档也基本够用）。

# 概念初识

## ①文件的几个概念

`（local）repository`：本地仓库

`workspace` 工作区

 `stage|index` ： `git add`但是没有`commit`的内容

![concept](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/1352126739_7909.jpg)

`remote （repo）`：远程仓库（常见的有：**github**、**gitee**（国内站点）、**gitlab**、**bitbucket**……）

[概念参考菜鸟教程](https://www.runoob.com/git/git-workspace-index-repo.html)

## ②reflog

`reflog` : 存放`git`操作的日志文件（下面的三个操作都是基于reflog的日志）

​		`undo`:撤销上一步的git操作 （**禁止操作上传到remote的git信息**）

​	    `redo` : undo的逆操作（**禁止操作上传到remote的git信息**）

​		`revert`：恢复某一部操作，如： `HEAD`切换到指定的commit上（commit内容是添加了两行代码），执行`revert`，则会将那两行代码删除（并且可以选择是否创建新的commit信息）

## ③branch&tag

> **注** branch的命令来自阮一峰的博客，并没有全部尝试。
>
> ​	`track`中文释义：足迹，踪迹

`branch` : 分支，简单理解成脱离主干的内容

![branch](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210201204823550.png)

```bash
git branch# 列出所有本地分支

git branch -r# 列出所有远程分支

git branch -a# 列出所有本地分支和远程分支

git branch [branch-name]# 新建一个分支，但依然停留在当前分支

git checkout -b [branch]# 新建一个分支，并切换到该分支

git branch [branch] [commit]# 新建一个分支，指向指定commit(此处的commit可以是hash)

git branch --track [branch] [remote-branch]# 新建一个分支，与指定的远程分支建立追踪关系

git checkout [branch-name]# 切换到指定分支，并更新工作区

git checkout -# 切换到上一个分支

git branch --set-upstream [branch] [remote-branch]# 建立追踪关系，在现有分支与指定的远程分支之间

git merge [branch]# 合并指定分支到当前分支

git cherry-pick [commit]# 选择一个commit，合并进当前分支

git branch -d [branch-name]# 删除分支

# 删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

`tag` : 标签，与分支类似

```bash
git tag # 列出所有tag

git tag [tag] # 新建一个tag在当前commit

git tag [tag] [commit] # 新建一个tag在指定commit

git tag -d [tag] # 删除本地tag

git push origin :refs/tags/[tagName]# 删除远程tag

git show [tag]# 查看tag信息

git push [remote] [tag]# 提交指定tag

git push [remote] --tags# 提交所有tag

git checkout -b [branch] [tag]# 新建一个分支，指向某个tag
```

> etc: 在`jQuery`中
>
> ​	**branch** 用于存放大版本的 `stable`即稳定的大版本代码。
>
> ​	**tag** 用于存放各个子版本。

`rebase` : 中文意思是变基，通常用户合并杂乱的分支信息，其副作用就是（清除分支的历史信息，使用时需要谨慎）

`.git`：文件夹，是一个默认为隐藏文件的文件夹，用于保存git信息。

`README.md`:在GitHub中会被默认渲染成页面的指定文件名的 md文件

​		[github提供的README.md文档](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/about-readmes)

`.gitignore`：文件，该文件语法包含的内容不会被上传的远程仓库，

​			[.gitignore模板](https://github.com/github/gitignore)

​			[github提供的.gitignore文档](https://docs.github.com/en/github/using-git/ignoring-files)

`HEAD`：相当于是鼠标的点击后被标记的含义（我看别人翻译为： **游标**），如：使用 `checkout`改变 `HEAD`的位置。

​					注：git内的 `HEAD`是唯一的：n个分支下也只有一个，即你切换了分支游标也走了。

```bash
# 解决.gitignore忽略文件误上传的问题
# 删除远程仓库的所有的node_modules文件
git rm -r -f --cached **/node_modules/ # -r就是remote的意思-f是force的意思
```

`LICENSE`: 用于描述你的代码可用权限，**图源见水印**。

![LICENSE](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/bg2011050101.png)

`hash`：每一次commit都会生成独一无二的hash用于某些操作，使用 `git log`（按下`q`退出**log**）看查看到`hash`，查看到指定 `hash`可以针对性的对某次commit做修改

# **常见命令**

## 建议

标注有**（本地）**命令含义：表示建议不要修改已经更新到remote的信息

![concept](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/git-command.jpg)

## 常见参数

`-a` all

`-m` message

`-d` delete

`-r` remote

`-e` edit

`-b` branch

`--abort`

## help

```bash
git --help # 读取命令帮助文档
git <command> --help # 打开帮助文档
git diff --help # 使用默认浏览器打开diff的帮助文档
```

## add

```bash
git add filename1 filename2 ……#手动指定文件，可以是一个也可以是多个
git add . # 提交所有已更改文件
git add *.c # 提交所有 .c结尾的文件名文件
git add -p # 分批次提交
```

## commit

>  `git commit`会进入vi文本编辑器，使用 `:q!`退出。
>
> ​		所以写入多行提交信息之前需要先学习：
>
> ​				1、 `vim`的基本操作。
>
> ​				2、`commit`规范。
>
> ​						[Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
>
> ​						[Angular提交信息规范](https://zj-git-guide.readthedocs.io/zh_CN/latest/message/Angular%E6%8F%90%E4%BA%A4%E4%BF%A1%E6%81%AF%E8%A7%84%E8%8C%83/)
>
> ​						[规范GIT代码提交信息&自动化版本管理](https://aotu.io/notes/2020/09/10/git-commit-control/index.html)
>
> ​				3、你也可以查找相关工具帮你完成规范的commitmsg协作。

```bash
git commit -m "<commit message>"
git commit # 输入多行的commit信息
```

### 值得一提

> ​	commit信息是可以触发GitHub某些行为的， **如:** 创建跳转到指定 `issue`的`commit`信息。
>
> ​		[commitevent的官方文档](https://docs.github.com/cn/developers/webhooks-and-events/github-event-types#commitcommentevent)你可以自行查阅，查找你需要的功能。

### 概念理解

>  命令相对于图形化客户端的含义。

`-m` 参数可以理解为是标题（`summary`）

不加 `-m`进入的是（`description`）

## clone

>  因为国内网络的限制`git clone`一个仓库需要十分漫长等待的时间。
>
> 常见的解决方式如下：
>
> ​			1、通过镜像站拷贝（`gitee`）拷贝镜像站点，然后从 `gitee`拉取。
>
> ​			2、一劳永逸：翻墙

```bash
git clone url <new filename> # clone 远程仓库到本地,可以指定文件名（通常可省略）
git clone -b [branchName] url # clone 指定分支
```

## **pull&push**

>  `pull`的使用是你所使用的代码远程仓库发生了 `git`信息冲突时使用，会覆盖你的本地信息。

```bash
git push # 将本地代码推送到远程仓库
git pull # 拉取远程代码的更新到本地
```

### 出现冲突

>  冲突：**conflict**

#### 方式1

>  个人项目可用使用，但是多人项目使用容易挨揍。

```bash
git push -f # 确定本地没有错误，慎用，坚定的（force）推送上去
```

#### 方式2

>  同时修改但是无代码层面的冲突（如添加了两个不同的函数），让git自动解决。

```bash
git pull # 会自动合并代码
git push

# 下面两个命令等效 git pull
git fetch # 拉取但是不合并
git merge # 修改完冲突之后合并
```

#### 方式3

>  手动合并冲突，即出现了修改同一处代码的问题。
>
> ​	一般 vscode的（`Git History`）插件会出现下面几个选项
>
> ​		1、保留a
>
> ​		2、保留b
>
> ​		3、让a、b同时存在
>
> ![conflict](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210201202737114.png)

```bash
git pull # 失败
```

```javascript
// user1
console.log("hey, man!")
```

```javascript
// user2
console.log("hello, little man!")
```

```javascript
// 此处选择让ab同时存在
console.log("hey, man!")
console.log("hello, little man!")
```

![example](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210201203504790.png)

过程总结：

```bash
1、修改冲突文件
2、git add . && git commit
3、push
```

## config

>  在上面**(初始本地配置)**中已经演示过如何设置邮箱和用户名了，下面演示常见命令。

```bash
git config --list # 查看配置列表
git config --list --global # 如果想查看全局的也可以添加上参数 --global
git config -e # 如果想要修改旧添加 -e参数
git config --global -e # 修改全局参数
```

## checkout（查看源码的神器）

>  通常被翻译为签出，可以形象的理解为从盒子里取出卡片的动作，移动了游标，使用变基可以回到主分支。
>
>  ​	![checkout](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210201212913704.png)

```bash
git checkout <branch name> # 切换分支
git checkout <commit 的hash> # 移动HEAD游标到指定commit
```

## **status**

> 需要事前强调的是： `git status`会预告一些你的可用命令。

![example](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210201200546482.png)

```bash
git restore --staged . # 撤销所有的 add文件
```

>  此状态是表示文件状态（下面的几种状态可能是在 `vscode`中才会出现的 ）
>
> ​	会有以下几种类型：
>
> ​		1、未修改\(**Origin**\)
>
> ​		2、已修改\(**Modified**\)&未追踪\(**Untracked**\)
>
> ​				修改：删除、增加、修改代码（只要是变动）
>
> ​				未追踪：文件层面上的修改（创建了的文件）
>
> ​		3、已暂存\(**Staged**\)  ：after `git add`
>
> ​		4、已提交\(**Committed**\)： after `git commit`
>
> ​		5、已推送\(**Pushed**\)： after `git push`

```bash
git status # 查看仓库状态，即查看你有哪些文件没有提交
```

## diff

>  非图形化界面会进入vi模式，使用 `hjkl`移动，`q`退出。
>
>  ​	输入`git diff --help`打开帮助文档
>
>  ​	输入 `gitk`查看`diff`信息

```bash
git diff # 比较工作区和暂存区的不同
git diff --cached [file]# 显示暂存区的指定文件和上一次commit的区别
git diff HEAD# 显示工作区与当前分支最新commit之间的差异
git diff [first-branch]...[]# 显示两次提交之间的差异
git diff --shortstat "@{0 day ago}"# 查看1天内提交了多少行代码
git blame <filename> # 列表展示指定文件的变化
```

> 下方代码的含义是（+）添加了`xx`，（-）删除了`aa`

```diff
+ xx
- aa
```

## mv & rm

>  `git mv` 与linux下的 `mv`使用方式一致，即可以用于**移动文件**也可以**重命名**文件，但是会多一个移入暂存区（`git add`）的效果。
>
> ​	`git rm` 同上，同样不要忘记正则匹配

```bash
 git mv <file-original> <file-renamed># 修改文件名并移入暂存区
 git rm <filename1> <filename2> ......# 删除工作区文件，并且将这次删除放入暂存区
```

## merge

>  合并分支的命令，**通常会有冲突:**需要手动根据冲突情况解决问题

```bash
# 首先进入main分支（如果已经在了就不用切换）
git checkout main

# 将test分支合并到main分支
git merge test

# 中断merge
git merge --abort

git merge --ff-only main #将当前分支合并到main分支并快速移动main分支到最新
```

## log&reflog

```bash
git log # 即查看git commit日志
git reflog # 查看git操作日志（用于 redo undo）
```

### log可选参数

>  `git log --argument`

```bash
gitk # 打开可视化的log查看工具
git log -S <keyword># 搜索关键词
git shortlog -sn# sort num,查看提交人并以提交次数排序
git log --name-status #每次修改的文件列表, 显示状态
git log --name-only #每次修改的文件列表
git log --stat # 每次修改的文件列表, 及文件修改的统计
git whatchanged #每次修改的文件列表
git whatchanged --stat  #每次修改的文件列表, 及文件修改的统计
git show # 显示最后一次的文件改变的具体内容
```

> 下图是截取自 `vue-next`项目的 `git shortlog -sn` 日志

![vue next commit log sort by num](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210131213745573.png)

## **remote**

> ​	 上方学习的命令都是基于本地仓库的操作，只要在前面添加上 `remote`即直接对远程仓库操作，但是不建议使用，下面列举使用较多的场景。

```bash
git remote branch # 查看远程（仓库）分支
```

# 变基（rebase）

>  万恶的变基，re变base基础，变更根基。
>
>  ​	好处：**commit history**十分干净。
>
>  ​	坏处：失去branch信息，还容易被人撕逼，所以需要依据团队标准使用。
>
>  ​			我们需要选学会 `git rebase --abort`中断rebase

### 1、branch

与 `merge`合并分支的方式不同，rebase合并的方式会删除被合并 `branch`的历史

​	可视化操作命令是

​		1、 `Rebase branch1 onto branch2`

​		2、鼠标 **右键** 点击最新的信息 `fast forward`让 `HEAD`移动到最新

```bash
# 命令行操作不太会
git checkout <分支名称>
git rebase --ff-only main # 变基到main并快速移动main分支到最新
```

### 2、pull rebase

pull 命令也可以使用变基

### 2、merge commit message

>  合并信息的限制：本次示例中的`git log`只有**5**条，所以合并的条数最大是**\(5-1\)**条即**4**条

​		使用场景：糊涂的程序员fix一个bug，一次`commit`没有完成，提交了10次 `commit`才完成，但是这10次`commit`仅仅做了这一件事，那么我们就可以将这10次`commit`合并为1次`commit`。

​		为什么说糊涂：脑子正常点也不会提交那么多次，只犯了一次 commit就可以选用amend啦。

<img src="https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20200717181219239.png" alt="before rebase" style="zoom: 67%;" />

<img src="https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20200717181556757.png" alt="after rebase" style="zoom:67%;" />

#### 方法1

```bash
# 合并最近四次commit信息,进入vim编辑器
$ git rebase -i HEAD~4 # 合并四条commit信息
```

```bash
pick 430a02b 第二次提交
s b70547d 第三次提交
s 00df675 第四次提交
s f70b17d 第五次提交
```

#### 方法2

```bash
# 进入vim编辑器,编辑commit id 内的所有子commit信息(不包含他本身)
$ git rebase -i [commit id]
```

#### 其他

> 进入vim后的文件翻译，即你修改头之外还有做其他事情。

```bash
# 命令:
# p, pick <提交> = 使用提交
# r, reword <提交> = 使用提交，但修改提交说明
# e, edit <提交> = 使用提交，进入 shell 以便进行提交修补
# s, squash <提交> = 使用提交，但融合到前一个提交
# f, fixup <提交> = 类似于 "squash"，但丢弃提交说明日志
# x, exec <命令> = 使用 shell 运行命令（此行剩余部分）
# b, break = 在此处停止（使用 'git rebase --continue' 继续变基）
# d, drop <提交> = 删除提交
# l, label <label> = 为当前 HEAD 打上标记
# t, reset <label> = 重置 HEAD 到该标记
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
```

```bash
# （重新回到）到rebase文件编辑
$ git rebase --edit-todo

# 保存rebase文件
$ git rebase --continue
```

# 常见操作

## amend（本地）

>  `amend`中文释义：修改；改善。
>
> ​	**适用场景:**上一次commit的内容实际未完成
>
> 使用方式：
>
> ​	step1：修改代码|文件
>
> ​	step2：
>
> ```bash
> git commit --amend -m "<新的提交信息>" # 信息可以不填
> git commit --amend
> ```

# 撤销三连

## undo&redo(本地)

>  只会gui操作，命令行操作自己查

## revert

>  生成新的commit信息完成前面的 `UNDO`，不会对过去的提交历史发生冲突

```bash
git revert <旧的提交hash>
```

## reset（本地）

>  reset的中文意思是重置，通常被理解为是 `git add`的可逆操作。

```bash
git reset HEAD . # 撤销全部 git add

git reset [file]# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变

git reset --hard# 重置暂存区与工作区，与上一次commit保持一致

git reset [commit]# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变

git reset --hard [commit]# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致

git reset --keep [commit]# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
```

# 暂存内容

## stash

>  暂存，与add命令移入暂存区不同，他移入的是另一个区域 stash（**并且永久存在**），需要手动删除，他在合并等（**可能发生冲突**）的时候也会为你生成stash。
>
>  ​	使用场景：
>
>  ​		需要切换分支，但是不想丢失修改，也不想使用 `git add`命令。
>
>  ​		**注:** pop 命令可以使用在任何一次的commit上，不仅仅是简单的使用在当前的分支上。

```bash
git stash save "<输入暂存的信息>"
git stash pop # 取出暂存，并删除暂存信息

git stash list # 展示暂存列表
git stash drop stash@{0} #删除列表1
```

# 可视化工具

>  **注:**在使用git可视化工具之前还是得学会基本的命令行操作
>
> ​	1、可视化工具在服务器上无法使用
>
> ​	2、软件的好处在于简单易用，但是同时带来了性能问题
>
> 个人推荐：简单的命令可以在命令行完成，查看 `diff`，查看、切换分支等需要hash的可以在可视化工具下完成。

[sourcetree](https://www.sourcetreeapp.com/)

[GitKraken](https://www.gitkraken.com/) **WIP**是 work in progress的缩写

[smartgit](https://www.syntevo.com/smartgit/)

[tortoisegit](https://tortoisegit.org/)

还有git自带的gui客户端（性能最好）

`visual studio code`的命令和插件（如果你是vscode用户，那么这种方式也是十分推荐的）

# 常见问题

## 1）需要每一次的`git push`都需要输入账号密码

```bash
#远程仓库提交方式版本
$ git remote -v

 #移除原始提交方式
$ git remote rm origin

#改用ssh
$ git remote add origin [ 仓库地址]

#设置跟随master，并提交到远程仓库
$ git push -u origin master
```

## 2）`release`|`merge`进程未中断

```bash
#中断rebase进程
$ git rebase --abort
#中断merge进程
$ git merge --abort
```

## 3）`git push`出现rejected错误

> 该错误是拒绝本地提交到远程仓库，原因是远程仓库的内容和本地仓库的内容冲突，据说是**非法篡改**

**解决方式①**

```bash
# 确定本地的代码没有问题，强制push
$ git push -f
```

**解决方式②**

```bash
# 确定远程仓库的代码没问题，拉取最新的内容再重写本地代码后git push
# 这两个命令合起来等效git pull
$ git fetch

$ git merge
```

```bash
# 获取远程仓库的更新
$ git pull
```

## 4）关于中文乱码问题

```bash
$ git config --global core.quotepath false          # 显示 status 编码
$ git config --global gui.encoding utf-8            # 图形界面编码
$ git config --global i18n.commit.encoding utf-8    # 提交信息编码
$ git config --global i18n.logoutputencoding utf-8    # 输出 log 编码
$ export LESSCHARSET=utf-8
# 最后一条命令是因为 git log 默认使用 less 分页，所以需要 bash 对 less 命令进行 utf-8 编码
```

## 5）`ls`打印中文目录是乱码

进入`Git\mingw64\share\git\completion`目录下打开`git-completion.bash`文件在末尾添上这么一行信息

```bash
alias ls="ls --show-control-chars --color"
```

## 6）如何生成在GitHub可以使用的目录

[gh-md-toc二进制文件下载](https://github.com/ekalinin/github-markdown-toc.go/releases)

1、下载这个gh-md-toc.windows.386.tgz

2、解压出来，并添加文件后缀 `.exe`

```bash
./gh-md-toc.exe <filename> # 生成目录
.\gh-md-toc README.md
```

> **tips:** 你可以更优雅的将该程序添加到你的环境变量中，并且用简短的命名。

## 7）如何更新git客户端

```bash
git --version
git update # 2.17.1版本的更新命令
git update-git-for-windows #  2.17.1版本之后的更新git的Windows命令
```

>  **注:**如果上述命令不存在，去git官网下载最新本覆盖安装。

## 8）Submodule 和 Subtree区别和使用

[Git 進階應用 Submodule 與 Subtree，使用它們來拆分專案](https://blog.puckwang.com/post/2020/git-submodule-vs-subtree/)

[Subtree 与 Submodule](https://gb.yekai.net/concepts/subtree-vs-submodule)