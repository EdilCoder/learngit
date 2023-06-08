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

