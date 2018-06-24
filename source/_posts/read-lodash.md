---
title: lodash部分源码阅读
date: 2018-06-24 09:33:06
tags: [源码解读,lodash]
---

> lodash 源码本身短小精悍 比较适合阅读，代码质量很高，涉及一些常见算法的应用。

### 函数方法

#### before
1. 调用方式
```
//_.before(n, func);
// 点击触发3次之后 将不再调用执行func
$(dom).on('click', _.before(4, func));
```
2. 实现
```
function before(n, func) {
  let result;

  return function (...args) {
    if(--n >= 1) {
      result = func.apply(this, args);
    } else {
      func = undefined;
    }
    return result;
  }
}

```
3. 知识点应用
    * 闭包保存参数n , func

#### after

1. 使用方法
```
//_.after(n, func)
// 在被调用n次的时候， 执行func
var saves = ['profile', 'settings'];
 
var done = _.after(saves.length, function() {
  console.log('done saving!');
});
_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
```
2. 实现
```
function after(n, func) {

  return function (...args) {
    if(--n < 0) {
      return func.apply(this, args);
    }
  }
}

```
3. 应用知识点
    * 使用闭包将n，func参数存储起来