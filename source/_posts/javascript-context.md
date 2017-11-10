---
title: js解析过程
date: 2017-11-09 19:38:59
tags: [javascript]
---

## js解析执行过程
分为两步：
1. 预解析 切换执行上下文 把［var声明的变量］和［function声明的函数］放到执行上下文(context)的变量对象(variables object)上，说白了就是创建存储空间。
  如果是在c等静态类型语言中， 我们在使用一个变量或者是函数之前 必须先声明 才能使用， 然而在js中 我们却可以在声明之前使用，其实这就是预解析的作用。

  ```
  alert(name) //undefined  不会报错
  var name = 'ngnice';

  say();//hello 不会报错
  function say(){
    console.log('hello')
  }

  ```
2. 执行js代码
  完成预解析之后， 才真正的开始执行代码， 所以上一步的操作 很像是把我们可能不规范的代码格式化成类似c（先声明，后使用）的规范的代码

> 这两个过程 在js加载完成之后的初始化执行，函数调用，eval执行都会发生

```
var name = 'ngnice';
function say(){
  var name = 'inner';
  console.log(name)
}

say()
```
1. 上面的代码执行的时候：先创建一个活动对象（预解析，规范化）

  ```
   VO ={
     name:undefined,
     say: function say(){ ... }
   }
  ```
2. 执行代码
  ```
  name = 'ngnice'//赋值
  say()//函数调用

  ```
3. 还记得吗 函数调用的时候也会进行上面的两个操作
  ```
  //预解析 声明变亮
  VO={
    name: undefined
  }
  //代码执行
  name = 'inner';//赋值
  console.log(name)//输出inner
  ```
参考：
1. http://www.cnblogs.com/yupeng/archive/2012/04/08/2437959.html

实战：
1. 面试题1
  ```
  function fn(a) {
    console.log(a);
    var a = 2;
    function a() {}
    console.log(a);
  }

  fn(1)
  ```

执行fn时候：
1. 进入fn函数的执行上下文，
2. 创建VO对象（函数中等同于AO）
  ```
    VO={
      arguments:{
        0:function a(){}
      }
    }

  ```
3. 执行

  ```
  console.log(a) //function a(){}
  a = 2 //赋值
  console.log(a)  //a
  ```

结论：

> 1. 参数赋值发生在预解析阶段，即：在预解析完成之后，参数的值就是参数的值 如果函数内部有和参数同名的函数声明 就会对参数的值进行修改；实际的效果就是同名的函数声明会覆盖掉实参的值（函数声明优先规则）
2. 函数内部和参数同名的变量 是参数的不同引用地址
3. 如果内部有和参数同名的变量声明 则不会对VO的同名属性造成影响


