---
title: git 常用命令
comments: true
tags:
  - git
categories:
  - GIT
date: 2017-09-09 10:36:59
update: 2017-09-09 10:36:59

---

# 版本间的切换

```
git log --pretty=online 版本记录

git reset -hard HEAD^ 会退上一个版本

git reflog 记录每一次命令，通过commitID可以回退

git reset --hard  commitID 回退到某个版本
git log 可以查看提交历史确认commitID
要重返未来，用git reflog 查看历史命令，确定版本。


```

# 三种回退文件修改内容

```
1. 修改文件，未暂存，git checkout -- file 丢弃工作区的修改
2. 修改文件，暂存 
git reset HEAD file 把暂存区的修改撤销掉
git checkout -- file 丢弃工作区的修改
3. 修改文件，暂存，已提交本地。使用版本回退。

git diff 查看修改与仓库的不同

提交之前撤销git add
如果只需要移除一个文件，那么请输入：
$ git reset <文件名>
移除所有没有提交的修改：
$ git reset

```


#关联远程分支
```
git remote add orgin git@github.com:仓库地址。
git push -u orgin master第一次推送master分支的所有内容，之后就可以使用 git push orgin master推送 最新修改。
```


# 创建并切换分支

```
git checkout -b newbranch 
创建分支
git branch newbranch 
切换分支
git checkout branch 
```

# 拉取远程分支，并创建本地之分

```
git checkout -b branchname  orgin/branchname 在本地创建和远程对应的分支
git fetch origin 远程分支名x:本地分支名x。   git checkout branch
```

# 合并分支(合并dev到当前分支)
git merge dev

# 查看分支

```
git branch 查看本地分支
git branch -r 查看远程分支
```

# 推送本地分支到远程

```
git push origin local_branch:remote_branch
git branch --set-upstream branchname orgin/branchname 建立本地分支与远程分支关联
```

# 删除分支

```
git branch -d newbranch
git branch -D newbranch(强删)
git push origin --delete <branchName>  删除远程分支
```

# 修复bug
```
创建分支，修复bug，合并，删除。当手上工作并没有完成时，先把工作现场git stash 储藏现场工作一下，修复完后切回本分支，再git stash pop,回到现场。
git stash list 查看储藏的工作现场
git stash apply 恢复stash的内容不删除
git stash drop 删除储藏的内容
git stash pop 恢复工作现场并删除

git remove -v 查看远程仓库的信息。
git push origin beanch-name 推送本地分支到远程仓库，如果推送失败，先git pull远程分支

```




# 修改错误的提交信息

```
git commit --amend -m ”YOUR-NEW-COMMIT-MESSAGE”
git push <remote> <branch> —force (修改推送后的提交信息)
```

# 标签

```
git tag 查看所有标签
git tag v1.0 打标签
git tag v1.0  committID 给指定分支打标签
git show v1.0 查看标签信息
git tag -d v1.0 删除标签
git push orgin v1.0 推送标签到远程分支
git push orgin --tags  推送全部尚未推送的标签
```

## 删除已推送的远程仓库的标签

```
git tag -d v1.0 删除标签
git push orgin:refs/tags/v1.0 
```



# 编写文档步骤

```git checkout master  
git pull
git checkout feature-add_insurance_docs  
git rebase origin/master  
git status  
vim  
git add .
git rebase —continue
hexo g
hexo s
 git push -f   
浏览器
merge 更新文档步骤
```




