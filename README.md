# 什么是git

git是一个分布式版本控制（ **distributed version-control**）系统。

更多git信息：[git的wiki](https://zh.wikipedia.org/wiki/Git) 

# git使用

## ①初始化本地配置
1、设置本地邮箱和账户名字(如果是你自己的电脑可以写入参数 `--gobal`)
```bash {.line-numbers}
git config user.name "<username>"
git config user.email "<email>"
```

2、生成ssh(sshkey生成器是git客户端自带的)
①`in bash terminal`

```bash {.line-numbers}
ssh-keygen -t rsa -C "<your eamil>"#这个步骤生成的sshkey路径会显示在终端，注意查看
```

②将生成的sshkey粘贴到github账户上（**此步是保证你的电脑自由使用ssh对该账户的仓库操作**）
`setting` -> `SSH GPG keys` -> `new SSH key`-> 粘贴上一步保存的sshkey并填写key名称


## ②通过 [github](https://github.com)初始仓库
### 方式1（推荐使用）

1、在GitHub上点击 `New repository` (choose `REAMDE.md`、`LICENSE`、`.gitignore`)

[.gitignore template](https://github.com/github/gitignore)
2、克隆上一步创建的远程仓库 `git clone url`

### 方式2

>  ​	需要**注意**的是：在 `2020/10/1`之后创建的GitHub仓库默认分支是 `main`而不是过去的 `master`。
>
> ​	当然你也可以自定义默认分支： `setting` -> `Repositories` -> `Repository default branch`填入 你想要的默认创建分支名，然后 `update`

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

# GitHub

>  GitHub提供免费的私有仓库托管服务，是时间上最好且毫无争议的开源网站，在2018年6月份被微软收购，题外话就是：npm也被微软收购 [参见营销号量子位的文章](https://www.qbitai.com/2020/03/12395.html)

[github中文文档](https://docs.github.com/cn) ：里面包含大量的GitHub知识：比起所谓的垃圾博客好一万倍，建议选择英文查看（当然中文文档也基本够用）。

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

​		`undo`:撤销上一步的git操作 （**禁止操作上传到remote的信息**）

​	    `redo` : undo的逆操作（**禁止操作上传到remote的信息**）

​		`revert`：恢复某一部操作，如： `HEAD`切换到指定的commit上（commit内容是添加了两行代码），执行`revert`，则会将那两行代码删除（并且可以选择是否创建新的commit信息）

## ③branch和tag

> **注** branch的命令来自阮一峰的博客，并没有全部尝试。
>
> ​	`track`中文释义：足迹，踪迹

`branch` : 分支，简单理解成脱离主干的内容

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
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

`tag` : 标签，与分支类似

> etc: 在`jQuery`中
> 	**branch** 用于存放大版本的 `stable`即稳定的大版本代码。
> 	**tag** 用于存放各个子版本

`rebase` : 中文意思是基变，通常用户合并杂乱的分支信息，其副作用就是（清除分支的历史信息，使用时需要谨慎）

`.git`：文件夹，是一个默认为隐藏文件的文件夹，用于保存git信息。

`README.md`:在GitHub中会被默认渲染成页面的指定文件名的 md文件 

​		[github提供的README.md文档](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/about-readmes)

`.gitignore`：文件，该文件语法包含的内容不会被上传的远程仓库，

​			[.gitignore模板](https://github.com/github/gitignore)

​			[github提供的.gitignore文档](https://docs.github.com/en/github/using-git/ignoring-files)

```bash
# 解决.gitignore忽略文件误上传的问题
# 删除远程仓库的所有的node_modules文件
git rm -r -f --cached **/node_modules/ # -r就是remote的意思-f是force的意思
```

`LICENSE`: 用于描述你的代码可用权限，**图源见水印**。

![LICENSE](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/bg2011050101.png)

`hash`：每一次commit都会生成独一无二的hash用于某些操作，使用 `git log`（按下`q`退出**log**）看查看到`hash`，查看到指定 `hash`可以针对性的对某次commit做修改

# 常见命令

## 建议

（本地）：表示建议不要修改已经更新到remote的信息

![concept](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/git-command.jpg)

## 常见参数

`-a` all

`-m` message

`-d` delete

`-r` remote

`-e` edit

`-b` branch

## help

```bash
git --help # 读取命令帮助文档
git diff --help # 使用默认浏览器打开diff的帮助文档
```

## add

```bash
git add filename1 filename2 ……#手动指定文件，可以是一个也可以是多个
git add . # 提交所有已更改文件
git add *.c # 提交所有 .c结尾的文件名文件
```

## clone

>  `git clone` 通常是很痛苦的事情，因为国内网络的限制导致`git clone`一个仓库需要十分漫长的时间。
>
> ​	解决方式如下：
>
> ​			1、通过镜像站拷贝（`gitee`）拷贝镜像站点，然后从 `gitee`拉取。
>
> ​			2、一劳永逸：翻墙

```bash
git clone url <new filename># clone 远程仓库到本地,可以指定文件名
```

## pull&push

>  `pull`的使用是你所使用的代码远程仓库发生了 `git`信息冲突时使用，会覆盖你的本地信息。

```bash
git push # 将本地代码推送到远程仓库
git pull # 拉取远程代码的更新到本地
```

>  `git push` 出现冲突

```bash
# 方式1
git push -f # 确定本地没有错误，慎用
# 方式2(这里需要保存你本地的修改)
git pull 
git push
# 方式3 （推荐使用）
git fetch # 拉取但是不合并
git merge # 修改玩冲突之后合并
```

## config

>  在上面已经演示过如何设置邮箱和用户名了

```bash
git config --list # 查看配置列表，
git config --list --global# 如果想查看全局的也可以添加上参数 --global
git config -e# 如果想要修改旧添加 -e参数
git config --global -e# 修改全局参数
```

## checkout

>  通常被翻译为签出，

```bash
git checkout <branch name> # 切换分支
git checkout <commit 的hash># 移动HEAD游标到指定commit
```

## status

```bash
git status # 查看仓库状态，即查看你有哪些文件没有提交
```

## diff

>  非图形化界面会进入vi模式，使用 `hjkl`移动，`q`退出

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

## reset

>  reset的中文意思是重置

```bash
git reset [file]# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变

git reset --hard# 重置暂存区与工作区，与上一次commit保持一致

git reset [commit]# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变

git reset --hard [commit]# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致

git reset --keep [commit]# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
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

>  合并分支的命令，**通常会有冲突：**需要手动根据冲突情况解决问题

```bash
# 首先进入main分支（如果已经在了就不用切换）
git checkout main
# 将test分支合并到main分支
git merge test
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
--stat # 查看文件变化
-S <keyword># 搜索关键词
git shortlog -sn# sort num,查看提交人并以提交次数排序
```

> 下图是截取自 `vue-next`项目的 `git shortlog -sn` 日志

![vue next commit log sort by num](https://zoulam-pic-repo.oss-cn-beijing.aliyuncs.com/img/image-20210131213745573.png)

## **remote**

> ​	 上方学习的命令都是基于本地仓库的操作，只要在前面添加上 `remote`即直接对远程仓库操作，但是不建议使用，下面列举使用较多的场景。

```bash
git remote branch # 查看远程（仓库）分支
```

## rebase

>  万恶的基变

1、与 `merge`合并分支的方式不同，rebase合并的方式会删除被合并 `branch`的历史

```
git rebase
```

2、他还可以合并提交信息

使用场景：糊涂的程序员fix一个bug，一次`commit`没有完成，提交了10次 `commit`才完成，但是这10次`commit`仅仅做了这一件事，那么我们就可以将这10次`commit`合并为1次`commit`。

```bash
git rebase -i HEAD~9
```

## amend（本地）

>  `amend`中文释义：修改；改善。
>
> ​	**适用场景：**上一次commit的内容实际未完成
>
> 使用方式：
>
> ​	step1：修改代码|文件
>
> ​	step2：
>
> ```bash
> git commit --amend -m "<新的提交信息>"
> ```

# 可视化工具

>  **注：**在使用git可视化工具之前还是得学会基本的命令行操作
>
> ​	1、可视化工具在服务器上无法使用
>
> ​	2、软件的好处在于简单易用，但是同时带来了性能问题
>
> 个人推荐：简单的命令可以在命令行完成，查看 `diff`，查看分支的情况等使用可视化工具更加舒服。

[sourcetree](https://www.sourcetreeapp.com/)

[GitKraken](https://www.gitkraken.com/)

还有git自带的gui客户端（性能最好）

`visual studio code`的命令和插件（如果你是vscode用户，那么这种方式也是十分推荐的）
