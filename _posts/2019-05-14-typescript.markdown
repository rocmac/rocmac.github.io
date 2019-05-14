---
layout: post
title:  Typescript
date:   2019-05-13 00:00:00 +0300
categories: typescript
tag: [typescript] # add tag
---

* content
{:toc}


最近在搞tutanota邮件客户端，大量使用了typescript，这里就将一些基本概念简单记录一下

## 几个要点：

- 微软出品，必属精品：TypeScript是由微软大神Anders Hejlsberg（安德斯·海尔斯伯格，丹麦人，Turbo Pascal编译器的主要作者，Delphi、C#开发领导者，同时也是.NET奠基人之一）领衔开发的
[typescript github 地址](https://github.com/Microsoft/TypeScript)
- IDE建议使用VS Code：最近微软拥抱开源的力度比较大，typescript和vs code都是开源产品，重点是vs code本身就是使用typescript开发的，简单一句话，用起来爽爽的，绝对不后悔
- Typescript 是 Javascript的超集：提供了类型系统和ES6的支持，可以编译为纯javascript

---

## Why Typescript

引用官网的内容

1. 增加了代码的可读性和可维护性

- 一句话，类型系统
- 编译阶段发现大部分错误
- 增强了编译器和IDE提示等功能，这也依赖于类型系统

2. 有容乃大

- 是JS的超集，.js直接命名为.ts即可使用
- 即使不定义类型，也可以自动根据上下文推断出类型
- 编译报错也可以生成Javascript，额。。。
- 兼容第三方库

---

## Typescript基础

### Hello Typescript

编译typescript->javascript

```
tsc hello.ts
```

VS Code中的terminal运行typescript

```
node hello
```

### 原始数据类型

原始数据类型包括：布尔值、数值、字符串、null、undefined 以及 ES6 中的新类型 Symbol

### any

```
let myFavoriteNumber: any = 'seven';
myFavoriteNumber = 7;
```

### 类型推断

刚有提到typescript会自动推断类型

以下代码会编译报错

```
let myFavoriteNumber = 'seven';
myFavoriteNumber = 7;

// index.ts(2,1): error TS2322: Type 'number' is not assignable to type 'string'.
```

### 联合类型

```
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

### interface

```
interface Person{
    firstName: string;
    lastName?: string;
}

let p = {
    firstName: 'Bruce',
    lastName: 'Lee'
}
```

### 数组

```
let fibonacci: number[] = [1, 1, 2, 3, 5];

let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

### 函数

```
// 函数声明（Function Declaration）
function sum(x, y) {
    return x + y;
}

// 函数表达式（Function Expression）
let mySum = function (x, y) {
    return x + y;
};
```

在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。

### 类型断言

```
function getLength(something: string | number): number {
    if ((<string>something).length) {
        return (<string>something).length;
    } else {
        return something.toString().length;
    }
}
```

### class

```
class Employee {
    public employeeName: string;

    constructor(name: string){
        this.employeeName = name;
    }

    greet() {
        console.log(`Good Morning ${this.employeeName}`);
    }
}

class Manager extends Employee {
    constructor(managerName: string){
        super(managerName);
    }
    
    delegateWork() {
        console.log(`Manager delegating tasks ${this.employeeName}!`);
    }
}

let m1 = new Manager('Brucee');
m1.delegateWork();
m1.greet();
```

