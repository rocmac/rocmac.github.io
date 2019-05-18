---
layout: post
title:  ssh 自动连接
date:   2019-05-18 00:00:00 +0300
categories: ssh
tag: [ssh] # add tag
---

* content
{:toc}


最近在玩微软的VS Code，刚推出了remote development功能，需要配置下ssh允许自动登录

## Client Side

id_rsa.pub: 公钥
id_rsa    : 私钥

目录: ~/.ssh/id_rsa.pub

生成SSH Key:

```
ssh-keygen -t rsa -b 4096
```

文件权限:

```
.ssh chmod 700 ~/.ssh
.ssh/config chmod 600 ~/.ssh/config
.ssh/id_rsa.pub chmod 600 ~/.ssh/id_rsa.pub
```

## Server Side

将本地SSH公钥添加到Server端

```
ssh-copy-id your-user-name-on-host@host-fqdn-or-ip-goes-here
```

文件权限:

```
.ssh chmod 700 ~/.ssh
.ssh/authorized_keys chmod 600 ~/.ssh/authorized_keys
```

搞定，可以命令行ssh直接连接了

```
ssh -p 22 jboss@1.1.1.1
```