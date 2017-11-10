---
title: shell基础
date: 2017-11-09 19:23:44
tags: [shell, linux]
---

### shell基础

#### 变量声明
```
name="ngnice"
echo $name
```
> TIPS
1. 直接变量 不需要其他的标识符标识是变量名称， 例如js中通过 var来定义变量
2.  引用变量通过 $your_varaiable
3. 赋值运算符前后不能有空格

#### 运算
```
//比较特殊的是数值运算
aa=1
bb=2
echo $aa+$bb//1+2 原封不动的输出 没有进行数值的加法运算

//使用expr  但是需要注意+前后必须要有空格
echo $(expr $aa + $bb) //3
//使用 $(())来实现  I like it~
echo $(($aa+$bb))
//使用$[]  同样不错
echo $[$aa+$bb]
```

