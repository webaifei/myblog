---
title: vim常见命令
date: 2017-11-08 14:22:21
tags: [vim]
---

### 光标
1. 回到上次编辑的位置
```
ctrl + o
ctrl + i
```
2. mark书签
```
m+[a-zA-Z] //定义书签
'+[a-zA-Z] //跳转到指定的书签
:marks //显示所有的书签
:delm[a-zA-Z] //删除指定的书签
:delm! //删除所有书签
```
