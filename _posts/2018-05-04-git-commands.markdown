---
layout: post
title:  git commands
date:   2018-05-04 00:00:00 +0300
categories: Git
tag: [Vue, router] # add tag
---

* content
{:toc}


====================

随便写写测试一下页面效果

====================

#### git 查看远程和本地分支代码

```
git branch -l
git branch -r
git branch -a
```

#### 切换分支

```
git checkout -b 
git checkout master
```

#### 删除远程分支

```
git push origin --delete 
```

#### 放弃修改

```
git checkout . #本地所有修改的。没有的提交的，都返回到原来的状态
git stash #把所有没有提交的修改暂存到stash里面。可用git stash pop回复。
git reset --hard HASH #返回到某个节点，不保留修改。
git reset --soft HASH #返回到某个节点。保留修改
```

#### 删除untracked file

```
git clean -nfd
git clean -fd
```

#### 删除本地修改

```
git reset --hard
git pull

git checkout HEAD file/to/restore
```

#### 展示保存本地修改

```
git stash
git pull
git stash pop
```

#### git add 撤销操作

```
git status 先看一下add 中的文件 
git reset HEAD 如果后面什么都不跟的话 就是上一次add 里面的全部撤销了 
git reset HEAD XXX/XXX/XXX.java 就是对某个文件进行撤销了
```


#### git 提交操作

```
git add . 

git add xx命令可以将xx文件添加到暂存区，如果有很多改动可以通过 git add -A .来一次添加所有改变的文件。注意 -A 选项后面还有一个句点。 git add -A表示添加所有内容， git add . 表示添加新文件和编辑过的文件不包括删除的文件; git add -u 表示添加编辑或者删除的文件，不包括新添加的文件

git commit -m "提交注释"

git push origin  分支名称，一般使用：git push origin master
```

