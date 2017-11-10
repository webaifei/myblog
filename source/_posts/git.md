---
title: git基本命令
date: 2017-11-09 19:50:44
tags: [git]
---
工作区－》暂存区－》本地仓库－》远程仓库

* clone已有的项目

```
git clone project-git-url
```
* 初始化一个新的仓库

```
git init
```
* 把新增的文件添加到我们的暂存区

```
git add xxx or .
```
* 把暂存区中的文件提交到本地仓库

```
git commit -m  'some msg for this commit '
```

* 推送到远程的仓库

```
//1 如果local_branch 不存在 会报错
//2. 如果省略了冒号和后面的远程分支名 代表远程分支名和本地分支名一样
//3. 如果远程分支名不存在的话 就会创建一个新的远程分支
//4. 如果local_branch 没写 是一个空格 那么就会删除远程分支
git push origin local_branch:remote_branch
```


* 我错误的提交了一些文件 怎么删除掉呢

```
git rm --cached xxx //从仓库中删除 而保留原文件
git rm -f xxx //从仓库中和本地删除文件（文件真实的被干掉了！！）
```

* 使用git reset 来进行版本的回退

```
 git reset --hard commit_id(某次的版本号)
 //HEAD 表示的是当前版本 ^表示上一个版本
 git reset --hard HEAD^
```
*git log 来查看历史commit的记录

```
  git log
  // 格式话输出
  git log --pretty=oneline

```
* git reflog 用来显示之前的操作记录

* git checkout -- xxx
1. 用来撤撤销add之后没有commit又进行的修改  满足两个条件： 1 add 了 2. 没有commit又进行了修改
2. 用来找回 已经add过误删的文件

* git checkout -t remote_branch // 用来从远程拉取指定分支 并且在本地新建同名分支 而且和远程分支已经关联


添加远程仓库

```
git remote add origin xxxx
```
把本地仓库的代码推送到远程仓库

```
 git push -u origin master
```

分支管理

```
git branch //列出所有分支
git branch -r //列出远程分支
git branch xxx//新建分支xxx
git branch -d xxx删除分支
git checkout xxx//切换到xxx分支
git checkout -b xxx //新建分支并切换到xxx分支
git merge xxx //合并xxx到当前分支
```


配置别名

```
git config --global alias.st status
```







