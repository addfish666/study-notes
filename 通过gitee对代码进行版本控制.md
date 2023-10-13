## 通过gitee对代码进行版本控制

`git init`

在当前目录下==初始化==一个Git仓库，该命令会在当前目录下==创建一个.git目录==，执行完该命令后就可以用Git进行版本控制



`git remote add origin <remote_repository_URL>`

将远程Git仓库与本地Git仓库==关联==，其中origin是远程仓库的==别名==，在之后执行Git相关命令后可以省略远程仓库地址



`git add .`

将当前目录下==所有变更==的文件添加到Git的暂存区



`git commit -m "消息"`

将提交的代码更改到==本地代码仓库==，并且提交了一条==提交信息==

> 直接`git commit`会进入到vim编辑器，按键盘i表示我们要插入的信息，按键盘的esc退出编辑模式，然后按:wq，表示保存并退出vim编辑器
>
> 上面两条命令可以合并写 `git commit -am "消息"`，一下从工作区跳到版本库



`git push origin master`

将本地的master分支推送到名为origin的==远程仓库==中



`git log`

用于查看历史提交

> 运行该命令之后，按q退出



`git remote -v`

用于查看本地仓库与哪些远程仓库有联系



`git fetch`

用于将远程仓库放到本地版本库



`git diff`

用于知道本地版本库与远程仓库的区别，在该命令的后面加上远程仓库名和分支名就可以看到区别了，例如`git diff origin/master`，查看之后发现没有问题可以通过`git pull`命令把远程仓库的内容直接整合到工作区



创建`.gitignore`文件可以用来让git忽略掉不需要提交的文件

![](../../../../typora所用截图/git.png)

## 补充

`git clone <repo>`

克隆仓库，`git clone https://gitee.com/addfishzjy/learning-materials.git`，执行该命令后，会在当前目录下创建一个名为`learning-materials`的目录，其中包含一个 `.git` 的目录，用于保存下载下来的所有版本记录。

如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：

`git clone https://gitee.com/addfishzjy/learning-materials.git my-learning-materials`



Git 全局设置:

```
git config --global user.name "曾家馀"
git config --global user.email "759804287@qq.com"
```

如果去掉 **--global** 参数只对当前仓库有效。



要更新你的本地仓库至最新改动，执行：
`git pull`
以在你的工作目录中 获取（fetch）并 合并（merge） 远端的改动。

将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。

```
git pull origin master:brantest
```

如果远程分支是与当前分支合并，则冒号后面的部分可以省略。

```
git pull origin master
```

上面命令表示，取回 origin/master 分支，再与本地的 brantest 分支合并。



## 分支管理

分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master 是“默认的”分支。在其他分支上进行开发，完成后再将它们合并到主分支上。

当你切换分支的时候，Git 会用该分支的最后提交的快照**替换**你的工作目录的内容



要合并其他分支到你的当前分支（例如 master），执行：
`git merge <branch>`

在这两种情况下，git 都会尝试去自动合并改动。遗憾的是，这可能并非每次都成功，并可能出现冲突（conflicts）。 这时候就需要你修改这些文件来手动合并这些冲突（conflicts）。改完之后，你需要执行如下命令以将它们标记为合并成功：
`git add <filename>`
在合并改动之前，你可以使用如下命令预览差异：
`git diff <source_branch> <target_branch>`

> 合并冲突发生在两个分支的相同文件的相同部分被同时修改，而合并操作无法自动解决这些修改的不一致。这时候，Git 将标记出冲突并在文件中显示冲突的部分，以便你手动解决。
>
> 在解决完所有冲突后，你需要使用 `git add` 将解决冲突的文件标记为已解决，然后使用 `git commit` 来提交这些修改，完成合并冲突的处理。



## 如何在github上面搜索项目

远程工作 remote job

面试题 awesome interview

> 通过左侧的语言来进一步筛选对应的面试岗位

免费书籍 awesome book

chatgpt资源 awesome chatgpt

> 搜索的终极技巧就是再需要搜索的前面加一个awesome



### 特殊的查找资源小技巧

常用前缀后缀

* 找百科大全 awesome xxx

> 比如 awesome vue

* 找例子 xxx sample

> 比如 vue sample，相当于找一个项目（例子）

* 找空项目架子 xxx starter / xxx boilerplate

> 省去从0开始配置一个项目的麻烦，相当于找样板项目

* 找教程 xxx tutorial



### 怎么去找开源项目

* https://github.com/trending/
* https://github.com/521xueweihan/HelloGitHub
* https://github.com/ruanyf/weekly
* https://www.zhihu.com/column/mm-fe
