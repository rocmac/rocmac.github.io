---
layout: post
title:  Sass basic concepts
date:   2019-04-02 00:00:00 +0300
categories: Front end
tag: [Sass, Css] # add tag
---

* content
{:toc}


### 概述
Sass的学名叫“CSS预处理器”，就是在CSS的基础上，引入了变量、嵌套、mixin（混合）、运算以及函数等功能，增加了代码的灵活性，可以让我们以更少的代码实现同样的效果，而且代码的整洁度、可读性更强

```
Sass有两种后缀名文件：.sass和.scss
```

### 编译方法
Sass编译方式大概有三种：通过命令行编译（基础方法）、GUI可视化图形同居编译及自动化编译。

## 基本用法
1. 变量
通过 $ 符号来定义，通过变量名称实现多处重复引用
```
$box-color: red;        //定义变量
ul{
    color: $box-color;      //引用
}
li{
    background-color: $box-color;       //引用
}

//编译后
ul {
  color: red;
}
li {
  background-color: red;
}
```

2. 嵌套

- 选择性嵌套
```
div {
    h1 {
        color: #333;
    }
    p {
        margin-bottom: 1.4px;
        a {
            color: #999;
        }
    }
}

 /* 编译后 */
div h1 { color: #333; }
div p { margin-bottom: 1.4px; }
div p a { color: #999; }
```

- 嵌套属性
```
div {
    border: {
      style: solid;
      width: 1px;
      color: #ccc;
    }
}

//编译后
div {
  border-style: solid;
  border-width: 1px;
  border-color: #ccc;
}
```

3. 代码重用之继承
```
.class1 {
    border: 1px solid #333;
}

.class2 {
    @extend .class1;
    background-color: #999;
}

//编译后
.class1, .class2 {
  border: 1px solid #333;
}

.class2 {
  background-color: #999;
}
```
4. 代码重用之Mixin混合器
```
@mixin mixName {        
    float: left;
    margin-left: 10px;
}

div {
    @include mixName;
}

//编译后：
div {
  float: left;
  margin-left: 10px;
}

```

5. 颜色函数
```
$box-color: red;        
ul {
    color: $box-color;      
}
li {
    background-color: darken($box-color,30%);       
}

//编译后：
ul {
  color: red;
}
li {
  background-color: #660000;
}
```

```
其他颜色函数

lighten(#cc3, 10%) // #d6d65c
grayscale(#cc3) // #808080
complement(#cc3) // #33c
```

6. import 引入
```
@import ‘partial’       //导入名为“_partial.scss”的文件
@import ‘toolbar.css’       //导入名为“toolbar.css”的文件
* {
    margin: 0;
    padding: 0;
}
```
