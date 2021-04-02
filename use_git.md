### Git

---

[廖雪峰教程](https://www.liaoxuefeng.com/wiki/896043488029600) 

##### git命令

```sh
# 初始化仓库
$ git init
# 把文件修改添加到暂存区 可反复多次使用，添加多个文件
$ git add <file>
# 把暂存区的所有内容提交到当前分支
$ git commit -m <message>
# 查看工作区的状态
$ git status
# 查看修改内容
$ git diff
# 删除文件
$ git rm <file>
# 关联远程库 origin 默认习惯命名 先有本地后有远程库
$ git remote add origin git@server-name:path/repo-name.git
# 从远程库克隆 先有远程库
$ git clone git@server-name:path/repo-name.git
# 推送master分支的所有内容 第一次加 -u
$ git push -u origin master
# 抓取分支
$ git pull
```

**远程库**：github或者git服务器

**工作区**：工作目录

**版本库**：.git隐藏目录，维护stage(暂存区)和master分支

![git_repository](./image/git_repository.jpg)


