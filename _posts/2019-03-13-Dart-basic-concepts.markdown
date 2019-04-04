---
layout: post
title:  Dart basic concepts
date:   2019-03-13 00:00:00 +0300
categories: Flutter
tag: [Dart, Flutter] # add tag
---

* content
{:toc}


### Dart的一些概念

---
- 每个变量都是一个对象
- Dart在运行前解析所有代码
- Dart支持类和对象里的函数，可以在函数里面创建函数
- 支持顶级变量，以及依赖于类或对象的变量
- 与java 不同，Dart不具备关键字public，protected和private。如果一个标识符以下划线(_)开始，那么他和他的库都是私有的
- Dart有两种运行模式：生产（production）和检查（checked）。我们建议在检查模式开发和调试，并将其部署到生产模式。
- Production mode是Dart程序一个速度优化的默认运行模式。Production mode忽略断言语句和静态类型。

--- 

### Dart内置标识符
为了方便javascript向Dart的移植


### Dart函数
  => 表达式;语法是{ return 表达式 }的简写。在printNumber()方法中，这个表达式调用了顶级函数print()。

```
void printNumber(num number) =>
     print('The number is $number.');
```

### 可选参数
可选参数可以是可选位置参数或者可选命名参数，但不能既是可选位置参数又是可选命名参数。

这两种可选参数都可以定义默认值。但是默认值必须是编译时的常量，比如字面值。如果没有为之提供默认值，那么该参数的默认值将会是 null。
- #### 可选命名参数

```

/// 把 bold 和 hidden 作为参数的值，并将默认值设为 false
enableFlags({bool bold: false, bool hidden: false}) {
     // ...
}

// bold 将会是 true， hidden 则是false
enableFlags(bold:true);

```

- #### 可选位置参数

```
String say(String from, String msg,
     [String device = 'carrier', String mood]) {
     var result = '$from says $msg';
     if (device != null) {
         result = '$result (in a $mood mood)';
     }
     return result;
}

assert(say('Bob', 'Howdy') == 
     'Bob says Howdy with a carrier pigeon');
```

### 级联操作符

```
querySelector('#button') // Get an object.
  ..text = 'Confirm'   // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

等于

```
var button = querySelector('#button');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```
