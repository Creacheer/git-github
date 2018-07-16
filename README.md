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

