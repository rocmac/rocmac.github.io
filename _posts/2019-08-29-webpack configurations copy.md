---
layout: post
title:  webpack configurations
date:   2019-08-29 00:00:00 +0300
categories: webpack
tag: [webpack] # add tag
---

* content
{:toc}


## webpack configurations

这里简单总结下webpack的常用配置，同时提交了一个示例工程可供下载使用

[https://github.com/rocmac/demo-webpack.git](https://github.com/rocmac/demo-webpack.git)

## 1. 什么是WebPack

WebPack可以看做是模块打包机:它做的事情是，分析你的项⽬目结构，找到JavaScript模块以及其它的⼀一些浏览器器不不能直 接运⾏行行的拓拓展语⾔言(Scss，TypeScript等)，并将其打包为合适的格式以供浏览器器使⽤用。

构建就是把源代码转换成发布到线上的可执⾏行行 JavaScrip、CSS、HTML 代码，包括如下内容。

+ 代码转换:TypeScript 编译成 JavaScript、SCSS 编译成 CSS 等。
+ ⽂文件优化:压缩 JavaScript、CSS、HTML 代码，压缩合并图⽚片等。 
+ 代码分割:提取多个⻚页⾯面的公共代码、提取⾸首屏不不需要执⾏行行部分的代码让其异步加载。 
+ 模块合并:在采⽤用模块化的项⽬目⾥里里会有很多个模块和⽂文件，需要构建功能把模块分类合并成⼀一个⽂文件。 
+ 自动刷新:监听本地源代码的变化，⾃自动重新构建、刷新浏览器器。 
+ 代码校验:在代码被提交到仓库前需要校验代码是否符合规范，以及单元测试是否通过。 
+ 自动发布:更更新完代码后，⾃自动构建出线上发布代码并传输给发布系统。

构建其实是⼯工程化、⾃自动化思想在前端开发中的体现，把⼀一系列列流程⽤用代码去实现，让代码⾃自动化地执⾏行行这⼀一系列列复杂的 流程。 构建给前端开发注⼊入了了更更⼤大的活⼒力力，解放了了我们的⽣生产⼒力力。

## 2. 初始化项⽬目

```
mkdir demo-webpack
cd demo-webpack
npm init -y
```

init指令会询问⼀一系列列的问题，并将你的配置写成⼀一个package.json⽂文件。如果使⽤用了了-f|--force|-y|--yes这些参数，那么 会⽣生成⼀一个默认的package.json⽂文件
设置npm仓库地址: 得到原本的镜像地址
npm get registry
> https://registry.npmjs.org/
设成淘宝的

```
npm config set registry http://registry.npm.taobao.org/ yarn config set registry http://registry.npm.taobao.org/
```

## 3.快速上⼿手

### webpack核⼼心概念

+ Entry:⼊入⼝口，Webpack 执⾏行行构建的第⼀一步将从 Entry 开始，可抽象成输⼊入。
+ Module:模块，在 Webpack ⾥里里⼀一切皆模块，⼀一个模块对应着⼀一个⽂文件。Webpack 会从配置的 Entry 开始递归找出所 有依赖的模块。
+ Chunk:代码块，⼀一个 Chunk 由多个模块组合⽽而成，⽤用于代码合并与分割。
+ Loader:模块转换器器，⽤用于把模块原内容按照需求转换成新内容。
+ Plugin:扩展插件，在 Webpack 构建流程中的特定时机注⼊入扩展逻辑来改变构建结果或做你想要的事情。 Output:输出结果，在 Webpack 经过⼀一系列列处理理并得出最终想要的代码后输出结果。

       Webpack 启动后会从Entry⾥里里配置的Module开始递归解析 Entry 依赖的所有 Module。 每找到⼀一个 Module， 就会根据配置的Loader去找出对应的转换规则，对 Module 进⾏行行转换后，再解析出当前 Module 依赖的 Module。 这些模块会以 Entry 为单位进⾏行行分组，⼀一个 Entry 和其所有依赖的 Module 被分到⼀一个 组也就是⼀一个 Chunk。最后 Webpack 会把所有 Chunk 转换成⽂文件输出。 在整个流程中 Webpack 会在恰 当的时机执⾏行行 Plugin ⾥里里定义的逻辑。

### 配置webpack & 创建目录

```
npm install webpack webpack-cli -D
mkdir src
mkdir dist
```

### 基本配置⽂文件

```
const path=require('path'); 
module.exports={
    entry: './src/index.js', 
    output: {
        path: path.resolve(__dirname,'dist'),
        filename:'bundle.js' 
    },
    module: {}, 
    plugins: [], 
    devServer: {}
}
```

+ 创建dist 
  + 创建index.html
+ 配置⽂文件webpack.config.js 
  + entry:配置⼊入⼝口⽂文件的地址 
  + output:配置出⼝口⽂文件的地址 
  + module:配置模块,主要⽤用来配置不不同⽂文件的加载器器 
  + plugins:配置插件
  + devServer:配置开发服务器器

```
const path=require('path'); 
module.exports={
    entry: './src/index.js', 
    output: {
        path: path.resolve(__dirname,'dist'),
        filename:'bundle.js' 
    },
    module: {}, 
    plugins: [], 
    devServer: {}
}
```

### 创建index.html⽂文件

在dist⽬目录下创建index.html⽂文件

```
<!DOCTYPE html>
<html lang="en"> <head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0"> <meta http-equiv="X-UA-Compatible" content="ie=edge"> <title>Document</title>
</head>
<body>
<div id="root"></div>
<script src="bundle.js"></script> </body>
</html>
```

## 配置开发服务器器

```
npm i webpack-dev-server –D
```

+ contentBase 配置开发服务运⾏行行时的⽂文件根⽬目录 
+ host:开发服务器器监听的主机地址
+ compress 开发服务器器是否启动gzip等压缩 
+ port:开发服务器器监听的端⼝口

## 支持加载css⽂文件

### 什么是Loader

通过使⽤用不不同的Loader，Webpack可以要把不不同的⽂文件都转成JS⽂文件,⽐比如CSS、ES6/7、JSX等

+ test:匹配处理理⽂文件的扩展名的正则表达式 
+ use:loader名称，就是你要使⽤用模块的名称 
+ include/exclude:⼿手动指定必须处理理的⽂文件夹或屏蔽不不需要处理理的⽂文件夹
+ query:为loaders提供额外的设置选项