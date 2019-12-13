### git学习

学习web：https://github.com/geeeeeeeeek/git-recipes/blob/master/README.md

#### 工作流

本地仓库的组成：

1. 工作目录，就是实际的文件
2. 缓存区(index)，临时保存改动
3. HEAD：指向最后一次提交的结果

#### 1. 创建代码仓库

- **git init**  将一个目录文件夹转为一个git仓库。 
- **git init <name> ** 新建一个空的git仓库
- **git init --bare <name>**  初始化一个裸的git仓库

普通库：除了.git目录之外，你还可以看到库中所包含的所有源文件。可以进行add、commit、delete等操作。

裸仓库：只有一个git目录。一般作为团队工作的共享库，大家可以往裸仓库里push自己的本地修改。一般会在名字后面加上.git。

- **git clone <repo> <name>** 将位于repo的仓库克隆到本地<name>目录下。<name>省略的话会新建一个目录。
- **git config** 配置git安装（或是一个独立仓库）

​	

#### 2. 保存更改

- **git add** 将当前的修改保存到git的缓存区。
- **git commit** 将缓存区的改动提交到本地的版本库
- **git diff** 对比两个文件的修改差异。
- **git stash** 将当前的工作状态保存到git栈。需要的时候再恢复。
- **.gitigonre** 忽略文件，操作的时候git会忽略配置的文件。



#### 3.检查仓库状态

- **git status** 显示工作目录和缓存区的状态。
- **git log** 显示的是已提交的东西。



#### 4.  检出之前的提交

- **git checkout** 主要是检出：检出文件、提交、分支。



#### 5.回滚错误的修改

- **git revert** 撤销一个已经提交的快照。会保留撤销前的提交。
- **git reset** 重设。只能从当前提交向前回溯。（**是一个比较危险的方式**）
- **git clean** 将没跟踪的文件从工作目录中移除。

​		

#### 6. 重写项目历史

- **git commit --amend** 将缓存的修改 和之前的提交合并到一起，并替换之前的提交。
- **git rebase** （传说中的变基哈哈哈哈哈哈哈哈哈）将分支移到一个新的基提交的过程
- **git reflog** 查看本地仓库的引用日志



#### 7. 保持同步

- **git remote** 创建、查看、删除和其他库之前的连接。
- **git fetch** 下载远程仓库的提交 存储为远程分支。



 