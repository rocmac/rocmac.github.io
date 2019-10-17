---
layout: post
title:  腾讯移动分析埋点
date:   2019-10-17 00:00:00 +0300
categories: React
tag: [埋点] # add tag
---

* content
{:toc}


## 背景

  最近有一些H5实现的广告推广任务，用React写了个Demo，需要统计一下广告推广的效果和相应的信息，发现国内有关H5埋点的介绍很少，大部分是关于IOS和Android埋点的介绍。
  
  而在前端发展迅猛的当前，H5埋点可以说是场景更多，国外的相应埋点平台就比较成熟，有完善的文档介绍和指引，youtube上也有相应的介绍，这里简单描述下腾讯移动分析平台的H5埋点。

## 腾讯移动分析

#### HTML5 SDK NPM版本

这部分找了好久终于找到，是在H5分析接入->高级功能 中的1.3，隐藏的有点深啊。

index.js中加入埋点的配置

```
import MtaH5 from 'mta-h5-analysis'

const store = createStore(rootReducer)

MtaH5.init({
  "sid":'500699610', //必填，统计用的appid
  "cid":'500699747', //如果开启自定义事件，此项目为必填，否则不填
  "autoReport":1,//是否开启自动上报(1:init完成则上报一次,0:使用pgv方法才上报)
  "senseHash":0, //hash锚点是否进入url统计
  "senseQuery":1, //url参数是否进入url统计
  "performanceMonitor":0,//是否开启性能监控
  "ignoreParams":[] //开启url参数上报时，可忽略部分参数拼接上报
});

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

#### 自定义事件上报

注意如果要自定义事件需要配置如下配置项，否则事件无法上报。另外腾讯移动分析自定义事件的详细信息是需要第二天才可以看到结果的

```
"cid":'500699747', //如果开启自定义事件，此项目为必填，否则不填
```

自定义上报数据格式：

```
MtaH5.clickStat("add_todo", {"userid":"www123"})
```

这里其实可以利用统计平台记录一些简单的统计信息，如H5页面中想要记录推荐人和电话等也可以用这种方式使用统计平台记录，自己无需单独开发后台应用记录这些简单信息了。