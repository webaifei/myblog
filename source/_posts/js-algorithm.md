---
title: js算法
date: 2018-05-20 16:03:52
tags: 算法
---

1. 求一个数组中最大的差值
```
1. 第一种实现方案：
先排序，然后最大值-最小值

2. 第二种实现方案：
遍历过程中找到最大的差值

function getMaxPro(arr){

    var minPrice=arr[0];
    var maxProfit=0;

    for (var i=0;i<arr.length;i++){

       var currentPrice=arr[i];

       minPrice=Math.min(minPrice,currentPrice);

      var potentialProfit =currenrPrice-minPrice;

       maxProfit=Math.max(maxProfit,potentialProfit);

     }
     return maxProfit;  

   }
```