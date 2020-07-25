# 命令行

## git init

初始化git仓库

## git add

添加文件 使用`.`添加所有文件

**温馨提示：对项目进行变更目录结构操作时，尽量使用`git mv`等命令进行更改，这样git可以同步跟踪变化**

## git commit

提交记录至本地仓库 使用-m快捷添加提交信息

提交的标题可以参考：
> [your name] [feat | fix | docs | style | refactor | test | chron] [comment]

其中：

+ feat：用户相关的新功能。构建脚本功能除外
+ fix：修正缺陷。构建脚本缺陷除外
+ docs：文档变更。
+ style：修正代码格式。
+ refactor：重构产品代码。例如变量重命名
+ test：添加或重构测试。不会更改产品代码
+ chron：更新构建脚本。不会更改产品代码

## git log

查看历史记录

## git diff

查看更改对比

## git checkout

两种用法

### 撤销更改

后跟文件名 可撤销更改 使用`.`撤销所有更改

### 切换、创建分支

+ checkout [branch] 切换分支
+ checkout -b [branch] 创建并切换至新分支
+ git branch [branch] 基于当前分支创建新分支

## git merge

合并某分支至当前分支

## git remote

查看远程信息 使用`-v`查询远程拉取和提交的地址

## git push

推送当前分支的本地修改至远程仓库。使用`-u`来指定当前分支所追踪的远程分支

> git push origin master

## git pull

拉取远程仓库

> git pull origin master

# 基本操作

## fork

从github或gitlab上fork到自己的帐号后再用git clone来拉取自己账号下的仓库并提交更改

### 如何拉取源仓库的最新提交？

使用`git remote add`指令添加一个新的远程仓库并拉取即可

> git add source [url]   
git pull source master

## git pull --rebase

参考：
> [简单对比git pull和git pull --rebase的使用](https://www.cnblogs.com/kevingrace/p/5896706.html)

简而言之 rebase简化了因merge而产生的菱形提交，减少分支，使得历史记录更加简洁清楚

注意rebase解决冲突之后使用`git rebase --continue`继续合并或`git rebase --abort`取消合并

## HEAD 是什么

参考：
> [Git中的‘HEAD’是什么？- Git名词解释](https://www.jianshu.com/p/4419f6a76005)

在 git 中，它是一个指向你正在工作中的本地分支的指针，可以将 HEAD 想象为当前分支的别名。

