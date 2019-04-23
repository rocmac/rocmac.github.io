---
layout: post
title:  nodejs调试问题定位
date:   2019-04-23 00:00:00 +0300
categories: nodejs
tag: [nodejs] # add tag
---

* content
{:toc}

[nodejs debug官方方法（包括本地调试和远程调试）](https://nodejs.org/en/docs/guides/debugging-getting-started/)
转了一圈发现看上面的文章就够了

### 使用webstorm调试

- 本地调试：run->debug 配置启动文件，然后打断点即可

- 远程调试：在Webstorm项目窗口中，打开Run/Debug Configurations窗口，点击 加号（+）选择“Attach to Node.js/Chrome”，启动配制。

---

最近在用nodemailer写邮件的相关功能，网上搜了下nodejs的调试工具，但是使用

```
npm install -g node-inspector
```

命令安装失败，报错如下：

```
node-pre-gyp ERR! Tried to download(undefined): https://node-inspector.s3.amazonaws.com/debug/v1.0.1/node-v64-darwin-x64.tar.gz
node-pre-gyp ERR! Pre-built binaries not found for v8-debug@1.0.1 and node@10.6.0 (node-v64 ABI, unknown) (falling back to source compile with node-gyp)
```

### 调试nodejs

安装 node-inspect，注意和 node-inspector 的细微区别，执行命令　npm install -g node-inspect. 然后输入　node --inspect server.js启动调试

打开 Chrome 浏览器，输入 chrome://inspect