Git is a distributted version control system.
Git is free software.
Git is good.
Try another way.
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


