---
layout: post
title:  Flutter issues
date:   2019-07-15 00:00:00 +0300
categories: Flutter
tag: [Flutter, emulator] # add tag
---

* content
{:toc}


## 问题

使用VS Code和Android Studio在真机上调试Flutter程序时偶尔会遇到安装卡住的问题（我使用的是华为Mate系列），尤其是安装后在手机删除App后重新安装，显示为：

```
Installing build/app/outputs/apk/app.apk...
```

卡住后只能新建一个Flutter项目，这时通常都是好的

## 解决方案

发现和IDE没啥关系，试了几次发现模拟器是可以正常启动的，所以怀疑还是国内Android手机ROM被修改导致的(当然我也没啥证据)

## 安卓模拟器

现在Genymotion也是不太靠谱，官网上很难能找到免费安装版本，只能Google了一下，才发现个人版免费下载链接：

[Genymotion个人免费版下载链接](https://www.genymotion.com/fun-zone/)