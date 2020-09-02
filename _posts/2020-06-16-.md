---
layout: post
title: sourcetree使用gitlab
date: 2020-06-16 00:00:00 +0300
categories: sourcetree & gitlab
tag: [sourcetree, gitlab] # add tag
---

- content
  {:toc}

## 现象

mac pro 笔记本装了 sourcetree 一直无法正常拉取代码，一直报 access denied，授权失败，最后发现是配置问题

## 解决方案

1. sourcetree 中添加账号，选择 gitlab 社区版，在 sourcetree 中生成 SSH 密钥
2. gitlab 中 ssh keys 中添加刚才生成的密钥
3. gitlab 中生成 access token，填到 sourcetree 中的密码进行验证
4. 最重要：sourcetree 中配置的 git 工具要选择使用系统安装的 git，这个浪费好长时间
