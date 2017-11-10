---
title: history对比hash 【前端路由】
date: 2017-11-09 19:29:10
tags: [前端路由]
---

pushState replaceState 对比hash切换

| option | h5 history | hash |
|-----|------|
| 只要不去点击刷新或者重新载入页面不刷新页面 | ✅ | ✅|
| 都能够产生history历史记录 | ✅ | ✅|
| 能够分享出去连接 传播性 | ✅ | ✅|
| 是否能被爬虫 | ✅（需要服务端对对应的路径进行相应） | ❌ |
| 服务端能够区别不同的请求路径 | ✅ | ❌ |
| 页面刷新的时候 服务端能够匹配不同的路径 返回首屏数据 | ✅ | ❌ |
| 页面刷新的时候 不需要服务端配置 | ❌ | ✅ |
| 触发window的popstate事件 |  ❌不能 通过js调用history.back() forward才触发|✅ |
| hashchange事件 | ❌ | ✅ |
| 是否能够操作history replace |✅|❌|


总结下：

> history api 对搜索引擎更加友好； 操作history有更大的权限； 我们能够选择不保留某个历史记录（通过replaceState） 缺点是需要服务端的配合；
<br>
hash更加的简单 前端能够通过hashchange 来判断不同的路由 进行不同的业务展示


注意点： window.onpopstate 事件的触发
1. 在通过history.back history.forward 等能触发
2. 在hash切换的时候也能触发

