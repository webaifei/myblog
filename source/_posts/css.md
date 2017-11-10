---
title: 一些不常用用的css写法
date: 2017-11-09 19:34:38
tags: [CSS]
---

#### font
按照如下的顺序书写
1. font-style
2. font-variant
3. font-weight
4. font-size/line-height
5. font-family


* 其中 属性4、5必须同时书写，其他的属性可以缺少（使用默认值） *
```
.title{
    font: 18px/26px Arial;
}
.titile-small{
  font: 600 14px/26px Arial;
}
```


#### 多行显示省略号 会使整个高度减少

#### line-height 文字居中 下面会多出一个px


