---
layout: post
title:  Immutable for javascript
date:   2019-09-02 00:00:00 +0300
categories: Javascript
tag: [Javascript] # add tag
---

* content
{:toc}


## Immutable for javascript

https://github.com/immutable-js/immutable-js

github将近3w个star不是闹着玩的^_^

官方文档：

https://immutable-js.github.io/immutable-js/

* 官方定义：

Immutable data cannot be changed once created, leading to much simpler application development, no defensive copying, and enabling advanced memoization and change detection techniques with simple logic. Persistent data presents a mutative API which does not update the data in-place, but instead always yields new updated data.

* 民间版本：

Immutable Data 就是一旦创建，就不能再被更改的数据。对 Immutable 对象的任何修改或添加删除操作都会返回一个新的 Immutable 对象。Immutable 实现的原理是 Persistent Data Structure（持久化数据结构），也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗，Immutable 使用了Structural Sharing（结构共享），即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点

* 个人版本：
  
高效深度拷贝，是拷贝不是引用

## 使用方法

```
npm install immutable
```

```
const { Map } = require('immutable');
const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set('b', 50);
map1.get('b') + " vs. " + map2.get('b'); // 2 vs. 50
```

## API介绍

其实几个典型的例子足矣：

```
const { Map } = require("immutable");
const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set('b', 50);
map1.get('b') + " vs. " + map2.get('b'); // 2 vs. 50
```

深度拷贝铁证例子：

```
const { Map } = require('immutable');
const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = Map({ a: 1, b: 2, c: 3 });
map1.equals(map2); // true
map1 === map2; // false
```

Javascript互转：

```
const { Map, List } = require('immutable');
const map1 = Map({ a: 1, b: 2, c: 3, d: 4 });
const map2 = Map({ c: 10, a: 20, t: 30 });
const obj = { d: 100, o: 200, g: 300 };
const map3 = map1.merge(map2, obj);
// Map { a: 20, b: 2, c: 10, d: 100, t: 30, o: 200, g: 300 }
const list1 = List([ 1, 2, 3 ]);
const list2 = List([ 4, 5, 6 ]);
const array = [ 7, 8, 9 ];
const list3 = list1.concat(list2, array);
// List [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

### Lazy Seq

用法：

```
const { Seq } = require('immutable');
const oddSquares = Seq([ 1, 2, 3, 4, 5, 6, 7, 8 ])
  .filter(x => x % 2 !== 0)
  .map(x => x * x);
```

