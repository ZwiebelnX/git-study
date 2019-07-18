## git command 的使用学习

因为之前都是使用IDEA或者其他IDE等git可视化插件进行git操作

如今在公司实习，我觉得使用git的命令模式进行操作能够更好地理解git的运作模式

于是创建本项目

不过我认为这篇文章对其他读者更多的意义是指导实践，这种东西还是自己试一下才能更加熟练



## 1、git clone和git push

git clone 从远程仓库克隆代码

git push 推送已经提交的代码

在push之前可以通过

```shell
git config --global user.name
git config --global user.email
```

来设置用户名和email

在某些系统内（如gerrit）中如果不设置这两个名称可能会导致无法推送

push时可能还会要求输入远程仓库等用户名和密码



## 2、git status

可以通过 git status来查看当前工作目录下的内容



## 3、git add

使用`git add`可以添加要被跟踪和提交的文件

使用`git add .`则可以添加当前仓库下的所有文件（除`.git`目录下的文件）

**温馨提示：对项目进行变更目录结构操作时，尽量使用`git mv`等命令进行更改，这样git可以同步跟踪变化**

除此之外，在commit之前通过`git add -u`来添加经过更改的文件，否则在commit时报无更改

学习使用git add进行文件添加

学习通过git commit和git push进行提交

