# git-github
Learning or do other things.<br>

## git学习

[廖雪峰的git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### Lessen 1 ：Add files to repository

（操作 -> 提交版本管理（Edition managenation））
* 添加文件：$ git add <file>
* 提交版本管理：$ git commit -m <message>

### Lessen 2 : Edition managenation

1.在修改文档后

* 查看仓库状态（有没有提交给坂本管理）：$ git status
* 查看修改后的和之前的差别：$git diff

2.版本回退

* 版本树（HEADtree）：HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id(or HEAD^ or HEAD~100)。

![something wrong](https://github.com/Creacheer/git-github/blob/master/picture/headtree.png)

* 穿梭前，查看版本树，以便确定要回退到哪个版本:$ git log
* 查看命令历史:$ git reflog

3.Working Direction & Storage Cache

* 工作区（repository）中有隐藏的版本库（.git），版本库中有暂存区，add先将改变存到暂存区，commit再将改动从暂存区的内容提交到当前分支中

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S1.png)

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S2.png)

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S3.png)

3.Manage Modification

* 没有add，即将修改从工作区添加到版本库的storage，在后面的commit时，修改就不会被提交到master（版本）里面

4.Undo edit

* 将working direction的修改撤销：$ git checkout -- <file>
* 将storage的修改回退到working direction（然后再重复上面的步骤即可撤销修改）：$ git reset HEAD（表示当前最新版本） <file>
* 假如已经提交版本，想撤销，则参考版本回退的内容（前提是没有提交到远程库）
* git status中的Changes not staged for commit就是指还没有add，即指working direction有修改，但storage没有commit，即没有提交进去；Changes to be committed指storage有修改，即没有上传到版本库中，需要git commit。
  
5.Delete Files


  
  
