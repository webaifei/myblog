---
title: MV*架构
date: 2017-11-06 15:51:18
tags: [mv*]
---

前端的洪荒时代只是提供表单提交验证等简单的功能，随着异步加载技术的出现，前端在客户端<=>服务器交互中扮演的角色越来越重要，其最终的目的是为用户提供更优的体验，同时也促进了前端职业化进程（我们不再只是切图仔！）在CS结构向桌面应用程序接近的同时，越来越复杂的业务逻辑使得前端人员开始思考将桌面应用的思想搬到前端实践中。

> 复杂的程序设计 必须有清晰合理的架构， 否则很难开发和维护

## 发展历程
### MVC
 应该是应用最广的架构模式了吧，或者说是最基本的架构模式，很多其他的模式都是基于它衍生而来。
    MVC 大家都了解， Model+View+Controller, 离用户最近的是View，这里接受用户的操作，给出反馈，然后View把相关的操作交给Controller，Controller去影响Model，然后再反馈到View，特点就是通信是单向的。

 但是实际过程中，可能比较灵活，因为前端开发中很大的工作量都在操作DOM。
 早期比较火的MVC库有[backbone.js](http://backbonejs.org/)

 当前火爆的[React](https://reactjs.org/) 以及 [vuejs](https://cn.vuejs.org/)
 其实将React和vuejs列入MVC框架中，不太妥当，两者都是用于构架ui层（view），并不包含模块加载，路由，数据管理，异步等utils集合。

### MVP
 将C替换成了P （presenter），他像一个控制调度中心，和View、Model进行双向通信，但是，View和Model之间不发生通信，这样 整个业务逻辑都在P这一层。
  前端实现库[riotjs](http://riotjs.com/)
### MVVM
 将P改成了VM（viewModel），基本上和MVP相同，不同的地方是VM和View之间双向绑定。
    比较流行的如： [angular.js](https://angularjs.org/)


## react 和 vuejs
|库|组件化|声明式|特殊语法|virtual dom|服务端渲染|难易程度|
|--|--|--|--|--|--|--|
|react|✔️|✔️|jsx|✘|✔️|相对概念较多|
|vue|  ✔️|✔️|✘  |✘|✔️|相对简单|

