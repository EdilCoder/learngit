Git is a distributted version control system.
Git is free software.
Git is good.
Try another way.
========================================

学习Git网站：
https://blog.csdn.net/mukes/article/details/115693833
https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576
学习的书籍：
Github入门与实践
========================================
初识Git：

创建 文件夹使用 $ mkdir filename
打开文件夹使用 $ cd filename
查看当前文件路径 使用 $ pwd

将当前目录变成Git可以管理的仓库使用 $ git init

创建编辑文本文件 $ vi readme.txt
在文件中 输入 i 可进行编辑
退出按 esc 在shift加：(冒号) 写入wq! 保存并退出

=========================================
将文件提交到仓库 $ git add readme.txt
备注修改内容 $ git commit -m "这里写修改简介"

每次修改都要上述两步

使用 $ git status 来查看当前仓库情况(是否提交)
例如：Changes not staged for commit: 修改过但没提交

使用 $ git diff 来查看修改具体内容是什么
==========================================

版本回退

查看都有哪些版本 $ git log
看着log太繁琐可以使用 $ git -pretty=oneline

使用 $ git reset --hard HEAD^ 回退到上一个版本(旧的版本) 回退到上上个版本是 HADE^^ 回退到上100个版本是 HEAD~100
使用 $ git reset --hard commit_id  再次回到最新版本

查看文件内容 $ cat readme.txt
找不到新版的 commit_id 使用 $ git relog 查看

==========================================
Git 底层是如何操作的

当编辑一个内容后 工作区生成一个除了readme.txt之外的新的文件 LICENSE
使用 $ git status 会提示我们 LICENSE 还没有被添加过 状态是 Untracked

当使用 $ git add 就把生成的LICENSE文件从工作区转移到 版本库中的 暂存区中(Stage)
当使用 $ git commit 就会把暂存区中 所有的修改提交到 版本库中的分区中(master) 指向master 的指针是 HEAD

工作区 --> 生成LICENSE --> git add --> 转移到暂存区(Stage) --> git commit--> 提交到分区(master)中

==========================================

管理修改

当修改一份文件后 使用 git add 将被放入 暂存区 之后再修改 再git add 再次放入 暂存区
在使用 git commit 将一起提交到分支 

如果 修改一次后 git add 再一次修改 再 git commit 只会将第一次修改的提交到分支
第二次修改的还在工作区 需要再次 git add git commit

===========================================

撤销修改

当编辑了不对的词时 想要销毁证据中使用

当编辑完文本 还在工作区，也就是没有 git add 时 使用 $ git checkout -- filename
当编辑完文本 再暂存区时， 也就是使用了 git add时 使用 $ git reset HEAD filename 然后会将修改记录返回至工作区 再通过上一步消除
当使用git commit 已经提交后也就是再本地仓库后 使用 $ git reset --hard commit_id 进行版本退回操作

注意：如果是想要消除太远的版本 就不可以

===========================================

删除文件==对文件进行操作

首先使用 vi filename 创建一个文件
再添加到暂存区和本地仓库中 $ git add filename $ git commit -m "添加了一个文件"
使用 $ rm filename 来删除文件
这时就从本地仓库退回到了 工作区 $ git status 查看状态 会告诉你哪些文件被删除了
现在可以使用 git rm filename 或者 git commit -m "删除了一个文件" 来进行删除或者记录删除

另一种情况是删错了，因为版本库里还存在 所以可以恢复到最新版本
git checkout 其实是用版本库里的版本替换了工作区的版本 无论工作区的修改还是删除 都可以一键还原
(删除只是一种操作命令，撤回只是撤回了删除的操作命令)
===========================================

远程仓库操作

添加远程仓库
1.注册一个github账号
2.在Git Bash中输入 $ ssh-keygen -t rsa -C "youremail@example.com" 用来创建SSH Key
通过 $ cd ~/.ssh 找到路径 并且用 $ pwd 查看路径
这时文件里有 id_rsa(私钥)  id_rsa.pub(公钥) 私钥不能泄露出去
3.登录GitHub 打开SSH Keys页面 添加公钥 可以使用 $ cat ~/.ssh/id_rsa.pub 来查看公钥 并且复制到github中
Title任意输入 之后Add Key 即可
 ---------

现在本地有了一个Git仓库 
又想在Github中创建一个Git仓库 并且让这两个仓库进行远程同步 这样就可以使得Github中仓库作为备份
也可以其他人通过该仓库来进行协作

1.登录Github 右上角添加按钮 找到“Create a new repo” 创建一个新的仓库
2.Repository name 填入 learngit 其他保持默认设置
3.Create repository按钮 创建

这就在github中创建好了 不过它是空的

我们可以从这个仓库中克隆出新的仓库 也可以把一个已有的本地库与之关联

在本地的 learngit仓库中 运行 $ git remote add origin git@github.com:你的github用户名/learngit.git
远程的仓库名叫做 origin 也可以叫别的

下一步就是把本地的库推送到远程库中
$ git push -u origin master 意思是 
把当前分支master推送到远程 第一次推送加 -u 不但会推送还会把本地mater和远程master关联起来

刷新github之后就同步了

之后只要在本地提交之后 通过命令
$ git push origin master 就可以推送至github了

---------------------------

查看远程库信息
$ git remote -v
删除远程库
$ git remote rm origin(使用远程库名称)

======================================

从远程(github)克隆仓库到本地

1.先登录github创建一个新的仓库，名字叫gitskills
2.勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件
3.新的远程库就创建好了，现在通过本地库克隆远程库

$ git clone git@github.com:你的github用户名/gitskills.git

这样本地也就有了一份远程的库

还可以通过这个地址去获取 https://github.com/你的github用户名/gitskills.git

但ssh协议快

========================================

分支管理

创建和合并分支

使用 $ git checkout -b dev 创建一个分支dev 并通过命令 -b 切换到该分支
单独只创建分支使用 $ git branch dev
单纯切换分支使用 $ git checkout dev

使用 $ git branch 查看当前分支

然后在dev分支中修改文本并提交

dev分支工作完成后再切换回 master分支
这时会发现刚在dev分支编辑的文本不见了 因为是在dev分支提交的

现在再把dev分支内容合并到master当中 $ git merge dev （在master分支中执行）
现在再查看文本就会有在dev分支中编辑的内容

合并完成后就可以删除分支dev了 $ git branch -d dev 
查看分支情况 $ git branch

----------

由于git checkout 同一种命令有两个作用 
所以创建并切换分支的功能使用  $ git switch -c dev
直接切换使用 $ git switch master


========================================

<<<<<<< HEAD
10.git log 可以查看分支合并情况
11.最后删除分支featurel
------以上是合并后，master与featurel合并的结构，再加以修改-------
解决分支冲突

1.创建新的分支featurel 编辑文本
2.提交
3.切换到master
4.在master改文本
5.master分支提交
6.合并 $ git merge 会发生冲突 两个分支文本内容不同 (git status也可以告诉我们有冲突)
7.必须手动解决冲突后再提交
8.重写修改文本并保存
9.再提交
10.git log 可以查看分支合并情况
11.最后删除分支featurel

使用这行来查看合并情况：
git log --graph --pretty=oneline --abbrev-commit

=======================================


