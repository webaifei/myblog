---
title: nginx基础
date: 2017-11-09 19:23:02
tags: [nginx]
---

## location匹配
> 按照匹配优先级顺序
1. =  精准匹配 完全匹配  比较适合匹配某个特定的路径
```
//只能匹配/index 其他的都不行，例如：/index/index.php
location = /index

```
2. ^~ 表示匹配普通字符串 前缀匹配

3. ~* 表示不区分大小写的正则匹配

4. ~ 表示区分大小写的正则匹配
