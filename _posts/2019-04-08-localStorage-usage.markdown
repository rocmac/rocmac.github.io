---
layout: post
title:  localStorage 用法
date:   2019-04-08 00:00:00 +0300
categories: HTML5
tag: [HTML5] # add tag
---

* content
{:toc}

### h5中解决cookie存储空间不足的问题

cookie存储空间：4k

localStorage存储空间：5M

### localStorage和sessionStorage区别与联系：

> 都用来存储客户端临时信息

> 都只能存储字符串类型的对象

> localStorage生命周期是永久，除非用户主动清除

> sessionStorage生命周期为当前窗口或标签页

> 不同浏览器无法共享localStorage或sessionStorage中的信息。相同浏览器的不同页面间可以共享相同的localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享sessionStorage的信息

### localStorage局限

1. 值类型限定为string
2. 隐私模式下不可读取
3. 本质上是对字符串的读取，存储内容过多会导致页面变卡
4. 不能被爬虫抓取

### 使用要点

需要先判断浏览器是否支持这个属性

```
if(！window.localStorage){
    alert("浏览器支持localstorage");
    return false;
}else{
    //主逻辑业务
}
```

三种写入方法

```
if(！window.localStorage){
    alert("浏览器支持localstorage");
    return false;
}else{
    var storage=window.localStorage;
    //写入a字段
    storage["a"]=1;
    //写入b字段
    storage.a=1;
    //写入c字段
    storage.setItem("c",3);
    console.log(typeof storage["a"]);
    console.log(typeof storage["b"]);
    console.log(typeof storage["c"]);
}
```

删除

```
var storage=window.localStorage;
storage.a=1;
storage.setItem("c",3);
console.log(storage);
storage.removeItem("a");
console.log(storage.a);
```


