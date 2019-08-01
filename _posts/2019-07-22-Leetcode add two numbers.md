---
layout: post
title:  Leetcode add two numbers
date:   2019-07-22 00:00:00 +0300
categories: Javascript
tag: [Javascript] # add tag
---

* content
{:toc}


## 概述

最近打算Leetcode走起，可以当做小游戏玩起来，现在越来越多的解题思路讲解，发现真是高手在民间，这种带动画的算法清晰明了，强力推荐

[动画版解题详解](https://github.com/azl397985856/leetcode)

## Add two numbers题解

话不多说，typescript版解题答案，ListNode是根据LeetCode给的方法改造的，也可以给后面其他提示复用

```
export class ListNode{
    val:number;
    next:ListNode;
    
    constructor(val?:number){
        this.val = val;
        this.next = null;
    }
}

var addTwoNumbers = function (l1:ListNode, l2:ListNode) {

    var carried = 0;
    const head = new ListNode(0);
    const noop:ListNode = {
        val: 0,
        next: null
    };

    let currentL1:ListNode = l1;
    let currentL2:ListNode = l2;
    let currentNode:ListNode = head;
    let newNode;
    let previousNode;

    while (currentL1 || currentL2) {
        newNode = new ListNode(0);

        currentNode.val = ((currentL1 || noop).val + (currentL2 || noop).val + carried) % 10;
        currentNode.next = newNode;
        previousNode = currentNode;
        currentNode = newNode;

        if ((currentL1 || noop).val + (currentL2 || noop).val + carried >= 10) {
            carried = 1;
        } else {
            carried = 0;
        }

        currentL1 = (currentL1 || noop).next;
        currentL2 = (currentL2 || noop).next;
    }

    if (carried) {
        // 还有位没进呢
        previousNode.next = new ListNode(carried)
    } else {
        previousNode.next = null;
    }

    return head;
};
```