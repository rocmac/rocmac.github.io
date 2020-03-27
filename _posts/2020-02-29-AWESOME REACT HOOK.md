---
layout: post
title:  AWESOME REACT HOOK
date:   2020-02-29 00:00:00 +0300
categories: REACT,GRAPHQL
tag: [FRONTEND] # add tag
---

* content
{:toc}


## 前言

过年，疫情赶一起，生平又多了一个经历，而且难忘，比印象中Sars那时候更加严重，管控更加严格，不知道是不是现在互联网传播信息太快的缘故。在家隔离了一段时间，陪孩子，陪家人，空闲时间做做自己的事情，竟然完全没有不自在的感觉，看来是宅男性格无疑了，也更加确认了将来的生活方式。

## REACT HOOK

由于项目中涉及到前后端接口的一些问题，如对老版本的兼容性问题，负责数据的查询问题。看了下FB的GraphQL比较能够解决当前的问题，就着手学习一下FB的开源项目，这里就介绍一下一些成熟的REACT HOOK，可以大大减少开发时间，这种语法糖真是欲罢不能。

如：
```
import React from 'react'
import { usePromise } from 'promise-hook'

const Demo = () => {
    const { isLoading, data } = usePromise(fetchURL, { resolve: true });
    return (
        <div>{isLoading ? <div>正在加载...</div> : data.site[0].title}</div>
    )
}
const fetchURL = () =>
    fetch(`http://www.***.com`).then(res => res.json());

export default Demo;
```

不需要自己实现异步接口等待的实现，可以直接拿过来使用，节省时间的同时减少自己开发bug的可能性

## 网址

[https://github.com/rehooks/awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks)

大家可以在这个网站上搜一搜，相信会有新发现