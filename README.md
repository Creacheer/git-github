# git-github
Learning or do other things.<br>

## git学习

[廖雪峰的git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### Lessen 1 ：Add files to repository

（操作 -> 提交版本管理（Edition managenation））
* 添加文件：`$ git add <file>`
* 提交版本管理：`$ git commit -m "<message>"`

### Lessen 2 : Edition managenation

1.在修改文档后

* 查看仓库状态（有没有提交给坂本管理）：`$ git status`
* 查看修改后的和之前的差别：`$git diff`

2.版本回退

* 版本树（HEADtree）：HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id(or HEAD^ or HEAD~100)`。

![->this](https://github.com/Creacheer/git-github/blob/master/picture/headtree.png)

* 穿梭前，查看版本树，以便确定要回退到哪个版本:`$ git log`
* 查看命令历史:`$ git reflog`

3.Working Direction & Storage Cache

* 工作区（repository）中有隐藏的版本库（.git），版本库中有暂存区，add先将改变存到暂存区，commit再将改动从暂存区的内容提交到当前分支中

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S1.png)

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S2.png)

![->this](https://github.com/Creacheer/git-github/blob/master/picture/W%26S3.png)

3.Manage Modification

* 没有add，即将修改从工作区添加到版本库的storage，在后面的commit时，修改就不会被提交到master（版本）里面

4.Undo edit

* 将working direction的修改撤销：`$ git checkout -- <file>`
* 将storage的修改回退到working direction（然后再重复上面的步骤即可撤销修改）：`$ git reset HEAD（表示当前最新版本） <file>`
* 假如已经提交版本，想撤销，则参考版本回退的内容（前提是没有提交到远程库）
* git status中的Changes not staged for commit就是指还没有add，即指working direction有修改，但storage没有commit，即没有提交进去；Changes to be committed指storage有修改，即没有上传到版本库中，需要git commit。
  
5.Delete Files

* 删除版本库文件（和add一样）：`$ git remove <file>, and $ git commit -m "<message>"`
* 假如被删除了（但库里面没有被删），可以恢复到最新版本：`$ git checkout -- <file>`
  
### Lessen 3 : Remote Repository

1.Add Remote Repository

* 将SSH key添加到远程服务端（Github），这样，Github就可以接收本地的通信
* 将本地的Repository添加到Github中：`$ git remote add origin git@github.com:michaelliao/learngit.git（其中michaelliao为Github账户名）`
* 把本地库的所有内容推送到远程库上：`$ git push -u origin master`
* 每个Repository进行前两步后，把本地master分支的最新修改推送至GitHub：`$ git push origin master`

2.Clone From Remote Repository

* 将网络Repository clone到本地：`$ git clone git@github.com:michaelliao/gitskills.git（michaelliao为Github的用户名）`
* git除了git：//的SSH协议，还支持https协议（使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。）：`$ git clone git https://github.com/michaelliao/gitskills.git（不确定）`
  
### Lessen 4 : Branch Management

1.Creat & Merge Branches

* 创建分支指针，并切换到分支指针（使HEAD指向分支指针）：`$ git checkout -b <name of branch> (= $ git branch <name of branch>; $ git checkout <name of branch>）`
* 查看分支：`$ git branch`
* 切回master：`$ git checkout master`
* 合并分支：`$ git merge <name of branch>`
* 删除分支：`$ git branch -d <name of branch>`

2.Conflict Resolution

* 当出现合并冲突时，可以在master里面手动修改冲突，再提交（本质其实就是普通的改变）
* 查看分支合并图：`$ git log --graph --pretty=oneline --abbrev-commit`

3.Branch Management Strategy

* 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。只需在合并分支时加上"--no-ff": `$ git merge --no-ff -m "merge without ff" <name of branch>`
* Strategy:Master主要用于新版本发布，平时干活在Branch上面，最后合并发布新版本。
 
![->this](https://github.com/Creacheer/git-github/blob/master/picture/BranchWork.png)

4.BUG Branch

* 修复BUG分支，通过创建新的BUG分支进行修复，然后合并删除
* 当前工作没有完成时（Working Direction和Storage Cache没有提交），通过stash功能先存储当前工作现场（因为所有分支共享Working Direction和Storagy Cache,在跳转到另一分支时并不会新建这两个区域并保存当前信息以便回来时恢复现场，所以需要手动完成这一步骤）：`$ git stach`
* 查看存储现场：`$ git stash lis`
* 恢复现场两种方式：<br>
  * 恢复后不删除stash内容，需`$ git stash drop`删除内容：`$ git stash apply( <stash编号，例如：stash@{0}>)`
  * 恢复并删除恢复的stash内容：`git stash pop`

5.Feature Branch

* Feature Branch是指每开发一个功能都建一个Feature分支，在上面开发。
* 没有合并的分支强行删除：`$ git branch -D feature-<name of branch>`

6.Mutiplayer Collaboration

* 当从远程仓库clone时，远程仓库的默认名称为`origin`，只默认clone`Master`分支，clone其他分支：`$ git checkout -b <name of branch> origin/<name of branch>`
* push branch：`$ git push origin <name of branch>`
* pull branch：`$ git pull`,假设pull失败（可能是因为最新版的branch和本地branch没有链接），需要和远程库branch链接：`$ git branch --set-upstreamto=origin/<name of branch> <name of branch>`
* 假如合并冲突，解决冲突，提交，再push

7.Rebase

* 将历史分叉合并为一个直线（但会导致commit修改版本基于的版本发生变化）：`$ git rebase`
 
### Label Management

1.Creat Label

* 先切换到需要打标签的分支上（否则就是当前分支当前commit），然后打标签：`$ git tag <Label>`
* 查看s所有标签：`$ git Label`
* 打以前commit的标签，需要查看历史提交的commit id：`$ git log --pretty=oneline --abbrev-commit`；然后再对目标commit id打标签：`$ git tag <标签> <commit id>`
* 查看标签信息：`$ git show <Label>`
* 创建有Description的标签：`$ git tag -a <Label> -m "<Description>" <commit id>`
  
2.Operations Of Label

* 删除Label：`$ git tag -d <name of label>`
* 推送单个标签到远程库：`$ git push origin <name of label>`
* 推送所有尚未推送的标签：`$ git push origin --tags`
* 如果标签已经推送给远程库，删除标签则需先删除本地标签，再从远程删除：`$ git push origin :refs/tags/<name of label>`

