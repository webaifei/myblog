---
title: 阻止表单默认行为
date: 2017-11-09 19:41:09
tags: [javascript]
---

1. 使用添加属性的方式绑定事件 有下面的两种方法

```
form.onsubmit = function (e){
   e.preventDefault();//method 1
   return false;// 2
}
```
2. 使用addEventListener添加的事件 只有一种方式

```
form.addEventListener('submit', function (e) {
        e.preventDefault();
    })

```
