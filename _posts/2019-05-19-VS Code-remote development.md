---
layout: post
title:  VS Code remote development
date:   2019-05-19 00:00:00 +0300
categories: ssh
tag: [ssh] # add tag
---

* content
{:toc}


## 概述
还是围绕最近微软推出的大杀器VS Code remote development，由于公司的服务器无法访问外网，而微软的remote development需要在Server端安装一些文件。所以我只能是找了公网的一台云主机测试一下

[VS Code remote development](https://code.visualstudio.com/docs/remote/remote-overview)

## 步骤

1. ### SSH autoconnect

    这个请见上一篇文章，简单配置一下即可

2. ### VS Code extension

    搜索下remote development，安装插件，安装一个会自动安装其他两个Remote - SSH和Remote -WSL，具体啥作用见官网

3. ### 配置.ssh/config

供参考

```
Host tencent_clout
    Hostname 127.0.0.1
    Port 22
    User ubuntu
    IdentityFile ~/.ssh/id_rsa
```

4. ### 连接
   
   可以在CONNECTIONS中看到这台主机了，右键就可以连接了，可以直接打开这台主机的目录，让人感觉是在本地开发的感觉，强力推荐。

5. ### 更多remote development功能待补充。。。