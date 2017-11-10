---
title: npm一些记录
date: 2017-11-09 19:35:15
tags: [npm]
---

* npm设置淘宝源

  ```
  1.在项目根目录下新建 .npmrc
  写入：
  registry = https://registry.npm.taobao.org
  2. npm config set registry https://registry.npm.taobao.org
  ```


* npm发布包 报错

  ```
  no_perms Private mode enable, only admin can publish this module: xxx

  修改npm源为 https://registry.npmjs.org 就行了
  npm config set registry https://registry.npmjs.org
  ```


