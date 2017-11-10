---
title: 执行上下文
date: 2017-11-09 19:38:22
tags: [javascript]
---

## 执行上下文

> 每当控制器进入ECMAscript可执行代码的时候，控制器就进入了一个可执行上下文。可执行上下文（简称EC）是一个抽象的概念，在ECMA262中用他来区分不同类型的可执行代码
```
我们定义一个可执行上下文的堆栈用数组表示
ECStack = []
```
可执行代码的类型：
1. js加载完成之后的初始化（就是我们平时放到最外层，window下执行的代码）会创建一个
```
ECStack = [
  globalContext
];
```
2. 函数执行 会把当前函数的执行上下文压入栈中，执行完成之后 再出栈销毁
```
//执行 push
ECStack = [
  globalContext,
  functionContext
];
//执行后 pop
ECStack = [
  globalContext,
  functionContext
];
```
3. eval 也会形成执行上下文


实例分析：

```
var name = 'ngnice'
function outer(){
  function inner(){
    console.log(name)
  }
  inner();
}

outer()
```
上面的代码执行的过程中的上下文变化：
1. 脚本加载完成初始化
```
ECStack = [
  globalContext
]
```
2. 执行outer函数
```
//push outerContext
ECStack = [
  globalContext,
  outerContext
]
```
3. 执行inner函数
```
//push innerContext
ECStack = [
  globalContext
  outerContext,
  innerContext,
]
```
4. 执行完毕inner
```
//pop innerContext
ECStack = [
  globalContext,
  outerContext
]
```
5. 执行完毕outer
```
//pop outerContext
ECStack = [
  globalContext
]
```
参考：
1. http://www.cnblogs.com/yupeng/archive/2012/04/07/2436616.html
