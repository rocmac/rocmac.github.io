---
layout: post
title:  Leetcode Merge k Sorted Lists
date:   2019-08-01 00:00:00 +0300
categories: Javascript
tag: [Javascript] # add tag
---

* content
{:toc}


## 概述

再来一道Leetcode题目，Merge k Sorted Lists，可以复用之前的Merge two sorted lists方法

## Merge k Sorted Lists题解

依然使用typescript，当然要在Leetcode上提交代码需要本地编译为javascript提交，这里强烈建议Leetcode支持Typescript另外越来越发现这个type的重要性和好处了，节省了很多后续定位问题的麻烦，想起了那句话“越自律，越自由”，有点跑题了，哈哈

这里要特别注意代码中的边界值，因为这个问题反复提交了好几次代码才通过

### Merge two sorted lists方法

```
var mergeTwoLists = function(l1:ListNode, l2:ListNode):ListNode {
    let res:ListNode = new ListNode(-1);
    let current = res;
    let i:ListNode = l1;
    let j:ListNode = l2;
    while(i && j && i.val !== undefined && j.val !== undefined){
        if(i.val <= j.val){
            current.next = i;
            i = i.next;
        }else{
            current.next = j;
            j = j.next;
        }
        current = current.next;
    }
    if(i && i.val !== undefined){
        current.next = i;
    }else{
        current.next = j;
    }
    return res.next || null;
};
```

### 解法一

自己码出来的，感觉代码稍显冗余，虽然不太美观，但可以解决问题，效率也不差

```
var mergeKLists = function(lists:ListNode[]):ListNode {
    if(!lists || lists.length === 0){
        return null;
    }
    let startP:number = 0;
    let endP:number = lists.length - 1;
    let resLists:ListNode;

    if(startP === endP){
        return lists[0];
    }

    while(startP < endP){
        let oddLists = mergeTwoLists(lists[startP], lists[endP]);
        resLists = mergeTwoLists(oddLists, resLists);
        startP ++;
        endP --;
    }

    if(startP === endP){
        resLists = mergeTwoLists(resLists, lists[startP]);
    }

    return resLists;
};
```

### 解法二

参考了网络上的答案，明显美观很多，用了位操作（早就还给老师了），同时分治递归解决

```
var mergeKLists = function(lists:ListNode[]):ListNode {
    if(lists.length === 0){
        return null;
    }
    if(lists.length === 1){
        return lists[0];
    }
    if(lists.length === 2){
        return mergeTwoLists(lists[0], lists[1]);
    }

    const mid = lists.length >> 1;
    const l1 = [];
    const l2 = [];
    for(let i=0; i<mid; i++){
        l1[i] = lists[i];
    }

    for(let i=mid, j=0; i<lists.length; i++, j++){
        l2[j] = lists[i];
    }

    return mergeTwoLists(mergeKLists(l1), mergeKLists(l2));
}
```