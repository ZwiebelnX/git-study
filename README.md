git-test rebase 1-2

给出两个比较好的参考：
> git-scm，官方教程与参考文档：[git-scm](https://git-scm.com/)
> 阮大神的博客，其中有各个方面的知识：[阮一峰的网络日志](http://www.ruanyifeng.com/blog/)


# 1、git clone

git clone 从远程仓库克隆代码

例如：

```shell
git clone https://github.com/ZwiebelnX/git_study.git
```

# 2、git status

可以通过 git status来查看当前工作git的工作状态

```shell
# 正式界面会更好看
位于分支 dev
您的分支领先 'origin/dev' 共 1 个提交。
  （使用 "git push" 来发布您的本地提交）

尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git checkout -- <文件>..." 丢弃工作区的改动）

        修改：     git_command_study.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

# 3、git add

使用`git add`可以添加要被跟踪和提交的文件

使用`git add .`则可以添加当前仓库下的所有文件（除`.git`目录下的文件）

**温馨提示：对项目进行变更目录结构操作时，尽量使用`git mv`等命令进行更改，这样git可以同步跟踪变化**

除此之外，在commit之前通过`git add -u`来添加经过更改的文件，否则在commit时报无更改

学习使用git add进行文件添加

# 4、git commit


通过`git commit`将暂存区的内容提交至仓库

```shell
# 快速commit方法
git commit -m '附言'
# 一般提交方法，适用于附言较多的场景，可以通过vim编辑附言
git commit
```

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


# 5、git push 

推送已经提交的代码

在push之前可以通过

```shell
git config --global user.name
git config --global user.email
```

来设置用户名和email

在某些系统内（如gerrit）中如果不设置这两个名称可能会导致无法推送

push时可能还会要求输入远程仓库等用户名和密码

# 6、git pull

从远端仓库拉取代码并通过`merge`或`rebase`合并到工作区。`git pull`命令相当于`git fetch` + `[git mrege | git rebase]`命令。

> 由于 git pull 的魔法经常令人困惑所以通常单独显式地使用 fetch 与 merge 命令会更好一些。

## git fetch

当 git fetch 命令从服务器上抓取本地没有的数据时，它并不会修改工作目录中的内容。 它只会获取数据然后让你自己合并。

## git merge

参考git-scm的文章

> [3.2 Git 分支 - 分支的新建与合并](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)

可能我们平时操作很简单，通过git merge <分支名>就可以进行合并。但直至读了上面的这篇文章，我才真正理解Merge的原理。

merge的合并过程可以分为以下两种：

### Fast-forward

当单纯移动HEAD就可以到达需要merge的分支的时候（如下图的hotfix分支），git也将会直接移动HEAD指向新的分支并将其合并。

以下图为例，hotfix分支的直接上游即是master的最后一个提交，所以直接移动HEAD不可能存在冲突。

![image](https://git-scm.com/book/en/v2/images/basic-branching-4.png)

这就是所谓的`Fast-forward`

### Normal-Merge

这是在多人开发中更容易碰到的情况

更一般地，两个分支可能会同时向前推进。当需要合并这两个分支的时候就没有办法直接移动HEAD来合并分支了。这时候所要做的工作将会复杂一点。

首先git会向前追溯至两个分支的共同祖先，如下图的`C2`，与当前两个分支的最后一个提交（下图的`C4`和`C5`）进行三方合并，并建立一个新的提交。
![](https://git-scm.com/book/en/v2/images/basic-merging-1.png)

合并后自动生成新的提交

![](https://git-scm.com/book/en/v2/images/basic-merging-2.png)


## git rebase

> 参考scm：[3.6 Git 分支 - 变基](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

![image](https://git-scm.com/book/en/v2/images/basic-rebase-3.png)

rebase将被合并的分支上的提交通过一定的逻辑合并到当前分支上，这样使得总体的提交看起来是一条线，十分已读。

但是注意，**rebase在将多个commit合并至当前分支时可能会穿插在当前分支的commit中间。** 这也造成了可能了可能会需要多次解决冲突。当两个分支相差过大时，使用merge合并来减少冲突次数是理想的选择。

rebase实际上的最终效果其实是和merge相差无几，但是rebase强调的是结果，而merge强调的是历史记录。这里贴出scm上对合并和变基的讲解。

除了拉直时间线合并分支以外，还会使用`rebase`修改某次提交的msg：

```shell
# 修改最近一次的commit信息
git commit --amend
# 修改倒数第三条的commit信息
git rebase -i HEAD~3
```



# 7、git reset和git checkout

参考下面这篇文章，是git-scm内的文章，讲的十分清晰和全面

> [7.7 Git 工具 - 重置揭密](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86)

其中有包括`git 三棵树模型`，以及git是怎么通过reset和checkout来对这三棵树进行操作

# 8、cherry-pick

合并其他分支的某些指定的提交

> [git cherry-pick 教程](http://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)

```shell
git cherry-pick <commitHash>
```
