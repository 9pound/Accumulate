# Git必知必会







git status  

显示 工作目录和暂存区的状态



working directory

git add 

来获取工作目录中的内容，并将其复制到索引中



git commit 

它会取得索引中的内容并将它保存为一个永久的快照， 然后创建一个指向该快照的提

交对象，最后更新 master 来指向本次提交



git reset

本质是撤销 git commit 操作



reset 命令会以特定的顺序重写这三棵树，在你指定以下选项时停止：

1. 移动 HEAD 分支的指向 （若指定了 *--soft*，则到此停止）
2. 使索引看起来像 HEAD （若未指定 *--hard*，则到此停止）
3. 使工作目录看起来像索引

--soft  移动head 回滚commit

--mixed 更新index 回滚 add commit

--hard  更新工作目录  强制覆盖工作目录





## 打标签

### 轻量标签

轻量标签很像一个不会改变的分支——它只是某个特定提交的引用。

轻量标签本质上是将提交校验和存储到一个文件中——没有保存 任何其他信息。

### 附注标签

存储在 Git 数据库中的一个完整对象， 它们是可以被校验的，其中包含打标签者的名字、电子邮件 地址、日期时间，

```bash
#查看标签
git tag

git tag -l

git tag -list

git tag -l  "v1.5*

#创建附注标签
git tag -a v1.4 -m  "my version v1.4"

#创建轻量标签
git tag v1.4-light

#给某个提交打上标签
git tag -a v1.4 9fceb02

#标签信息和与之对应的提交信息
git show v1.4

#默认情况下，git push 命令并不会传送标签到远程仓库服务器上。
#在创建完标签后你必须显式地推送标签到共享服务器上。
git push origin <tagname>

#会把所有不在远程仓库服务器上的标签全部传送到那里
git push origin --tags


#删除标签,不会从远程仓库中移除这个标签
git tag -d <tagname>

#删除远程仓库标签
git push <remote> :refs/tags/<tagname>

git push origin --delete <tagname>

#检出标签
#这会使你的仓库处于“分离头指针（detacthed HEAD）”的状态，在“分离头指针”状态下，如果你做了某些更改然后提交它们，标签不会发生变化， 但你的新提交将不属于任何分支，并且将无法访问，除非通过确切的提交哈希才能访问。
git checkout v2.0.0

#检出标签并创建新分支
git checkout -b version2 v2.0.0





```



## 远程仓库

```shell
#查看远程仓库地址
git remote -v
origin  git@github.com:jekip/naive-ui-admin.git (fetch)
origin  git@github.com:jekip/naive-ui-admin.git (push) 

#设置远程仓库地址
git remote set-url origin git@github.com:9pound/naive-ui-admin.git

```



## 撤销操作

```shell
#取消暂存(add)
git reset HEAD <file> 

 
#撤销对文件的修改、对file 的本地修改都会消失
git checkout --<file>


#补充commit
git commit --amend
```

### 回退

```shell





#线上回退了、强制更新本地分支
git reset --hard origin/master
```

