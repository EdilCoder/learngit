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

分支管理策略

如果直接合并 git merge 
那么Git 会直接使用 Fast forward模式
这种模式下 删除分支 会丢失分支信息

所以这次合并使用 --no-ff -m 的模式 可以对合并备注合并分支信息

1.创建一个分支 编辑文本
2.提交
3.回到master
4.合并 $ git merge --no-ff -m "合并分支信息" dev
5.查看分支合并情况git log --graph --pretty=oneline --abbrev-commit

---分支策略---

master分支应该是非常稳定的 仅用来发布新版本 平时不能再上面干活

干活都在dev上面 当1.0版本发布时 再把dev分支合并到master上面

团队合作：

master---------------
      `---dev--`---dev
         `      `--Tom-----
	  `---Jack-----

Tom和Jack一般都是在dev上干活，时不时的往dev分支合并就可以了

========================================

Bug分支 修复处理方法

假设现在正在dev分支中编辑一个文本文件
由于还有没写完不能提交(add, commit)

突然接到一个紧急的Bug要修复 issue-101 但dev还没提交

所以用 $ git stash 功能 将当前的工作区存藏起来 等修复完bug再继续工作

$ git status 查看工作区情况

假定需要修复的是master中的分支 就从master 创建临时分支

$ git checkout master 转到master分支
$ git checkout -b issue-101 创建issue-101分支 
接下来在文本中修改编辑
然后提交(add commit)

修复完成！

---回到dev 继续工作--

$ git switch
$ git status 这时候工作区是干净的 因为存藏起来了

$ git stash list 查看在哪里
$ git stash pop 恢复到工作区的同时 把stash中的内容删了
$ git stash apply 单纯恢复到工作区 但并不删除stash中的内容
$ git stash drop 来清除stash中的内容

可以多个存藏与stash中
并恢复指定的stash
$ git stash apply stash@{0}

---回到dev之后有一个问题---

修复的文件是master的文件 
修复好后master更新了
但是dev中的readme.txt是修复前的 master文件 

所以我们要更新dev中的 readme.txt 文件
首先要在master分支当中 使用log找到 issue-101 的 commit_id (一串字母数字 前五位即可)
然后返回dev中

使用$ git cherry-pick commit_id(上一步的一串数字字母) 复制特定的提交到当前分支中
这样就可以了，既可以有完整的备份也可以继续工作并上传提交合并


====================================

Feature分支

在实际开发过程中,总有新功能不断添加进来
为了不把主分支搞乱了 没添加一个新功能就加一个feature分支 完成后再合并
最后删除这个分支

假设添加一个新功能 开发代号为Vulcan 该任务用于下一代飞船

$ git switch -c feature-vulcan

...五分钟后开发完毕，vulcan.py

$ git add vulcan.py 提交
$ git commit -m "add feature vulcan"

切换回dev 准备合并
一切顺利的话 feature和bug分支类似，合并然后删除
但此时上级通知 新功能必须取消 因为经费不足

$ git branch -d feature-vulcan 删除分支
$ git branch -D feature-vulcan -D是强行删除

=======================================

多人协作【重要】

什么是多人协作？

在github中有一个项目库
有两个为此项目贡献的人 EdilCoder 和 yedel123
这个github项目的发起者是 EdilCoder
yedel123是来帮忙的(因此首先需要自己的github)

在同一台电脑模拟(需要在另一个目录下克隆)

--具体操作--

1.在EdilCoder(learngit库)中查看 远程库的信息
$ git remote -v

origin  git@github.com:EdilCoder/learngit.git (fetch)
origin  git@github.com:EdilCoder/learngit.git (push)

2.推送分支到远程库中(EdilCoder本地库)
$ git push orgin master

3.推送其他分支 比如dev(EdilCoder本地库)
$ git push orgin dev

什么库值得推送？
master分支是主分支，因此要时刻与远程同步
dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步
bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug
feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发

4.因为是模拟另一人，不过是在同一电脑中操作的

a.打开另一个Git bash窗口 我这里是 d/learngit2 原来的是d/learngit

b.在d/learngit2 中将github中EdilCoder的数据拷贝到自己的库中

$ git clone git@github.com:EdilCoder/learngit.git

c.克隆好了之后进入 d/learngit2/learngit 中(cd learngit)
这时候 git branch 查看分支就会发现只能看到master分支

5.在对yedel123的仓库 d/learngit2/learngit 操作前
【确保】在 EdilCoder的仓库 d/learngit 中进行了【推送分支dev】的操作
否则会报错： 
fatal: 'origin/dev' is not a commit and a branch 'dev' cannot be created from it

6.在yedel123的库 d/learngit2/learngit 中执行
$ git checkout -b dev origin/dev 
因为yedel123也要在 dev分支上开发
所以必须创建远程origin的dev分支到本地

现在就yedel123就可以在dev分支上进行编辑了

7.创建一个文本文件 vi env.txt(yedel123的库 dev分支中)
编辑文字 This is env. 保存退出
add commit 进行提交

8.进行上传远程的操作 
$ git push origin dev
这时yedel123 帮助 EdilCoder 编辑了一份文本文件

9.这时EdilCoder也正好在自己的库中dev分支中编辑文本文件
vi env.txt 并且编辑了文本 之后提交 add commit
之后 git push origin dev 时显示冲突 发生了错误

错误如下：
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

这是因为yedel123最新提交和EdilCoder推送的提交有冲突

10.解决办法

$ git pull 把远程端的提交从 origin/dev 抓下来，然后在本地库合并，解决冲突，再推送

但还是失败了，失败原因如下：

原因是没有指定本地dev分支与远程origin/dev分支的链接 

There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev

11.根据上面提示 设置dev和origin/dev的链接

$ git branch --set-upstream-to=origin/dev dev

然后再 git pull

12.这回成功拉下来，但是有合并冲突

提示如下：

Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.

13.可以用 git status 查看哪个文件发生了冲突
然后 vi env.txt 编辑冲突
再提交 add commit -m "fix env commit"
最后进行 git push origin dev 上传至远程

总结：

1.可以试图用 git push origin branch_name 推送自己的
2.如果推送失败，则因为远程分支比你本地更新一点，需要先用git pull试图合并
3.如果合并有冲突，则先解决冲突，并在本地提交
4.没有冲突或者解决冲突后再用 git push origin branch_name推送！

！！如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>

--删除命令--

删除指定的远程仓库
git remote rm origin

删除远程的分支
git push origin --delete branch_name

删除远程的tag
git push origin --delete tag <tagname>

删除本地仓库
ls -a 找到目录.git
rm -rf .git 删除


==================================


