
## git 查看某个文件的版本历史


git log -- controllers/price/coupon.py
git log -p controllers/price/coupon.py

git log --follow controllers/price/coupon.py


### 使用 tig

[tig](https://github.com/jonas/tig)

tig controllers/price/coupon.py
在项目目录下：
tig查看git 的 log

常用指令：
上下箭头选择log的版本
enter进入具体版本查看详细
k和j是上下滚动查看详细信息的内容
m是关闭详细信息，返回到log的版本
pageup/pagedown是同k和j，只不过是一屏一屏的滚动




## git 查看某个文件两个版本之间的差异

git diff HEAD^^ HEAD main.c
git diff <revision_1>:<file_1> <revision_2>:<file_2>




## Reference

[How to diff the same file between two different commits on the same branch?](http://stackoverflow.com/questions/3338126/how-to-diff-the-same-file-between-two-different-commits-on-the-same-branch)

[View the change history of a file using Git versioning](http://stackoverflow.com/questions/278192/view-the-change-history-of-a-file-using-git-versioning)

[The Tig Manual](http://jonas.nitro.dk/tig/manual.html)



