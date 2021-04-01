[廖雪峰教程](https://www.liaoxuefeng.com/wiki/896043488029600)

初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；把文件修改添加到暂存区
2. 使用命令`git commit -m <message>`，把暂存区的所有内容提交到当前分支。

查看工作区的状态：

- 使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

命令`git rm <file> `用于删除一个文件。

**工作区**：工作目录

**版本库**：.git隐藏目录，维护stage(暂存区)和master分支

![git_repository](E:\repository\learning\image\git_repository.jpg)



##### 远程库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

从远程库克隆`git clone git@server-name:path/repo-name.git`