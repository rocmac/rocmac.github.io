---
layout: post
title:  typescript tips
date:   2019-08-10 00:00:00 +0300
categories: Typescript
tag: [Typescript] # add tag
---

* content
{:toc}


## 概述

使用Tyepscript需要注意的一些事项或小技巧，权当记录一下备忘

## typescript tips

candidates升序排序

```
candidates:number[]
candidates.sort((a, b) => a-b)
```

扩展运算符 ...

```
function backtrackNumber(list:number[][], tempList:number[], nums:number[]):number{
    if(tempList.length === nums.length){
        return list.push([...tempList]);
    }
    for(let i=0; i<nums.length; i++){
        if(tempList.indexOf(nums[i]) != -1){
            continue;
        }
        tempList.push(nums[i]);
        backtrackNumber(list, tempList, nums);
        tempList.pop();
    }
}
```

Array clone

```
const oMatrix:number[][] = JSON.parse(JSON.stringify(matrix));
```

String sort

```
    function sort(str:string){
        return str.split("").sort().join("");
    }
```

Object.values:一个包含对象自身的所有可枚举属性值的数组

```
(<any>Object).values(hashTable);
```

Array过滤null和undefined

```
intervals.filter(q=>q)
```

位运算符取中间值

```
const mid = start + ((end - start)>>1);
```

