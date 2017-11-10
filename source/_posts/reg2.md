---
title: 正则实战
date: 2017-11-09 19:40:30
tags: [正则]
---
## 实战
> 纸上得来终觉浅 绝知此事要躬行

** 下面的实例都是简单的校验（前端一般够用）**
1. 手机号

  ```
  // 规则：
  /*纯数字 1开头 第二位34578 总共11位*/
  var telReg = /^1[34578]\d{11}/
  ```
2. qq号

  ```
  //规则：
  /*纯数字 非0数字开头 最少4位*/
  var qqReg = /^[1-9]\d{4,}/
  ```
3. 邮箱
  ```
  //规则：xxx@xx.xxx
  /*1. 肯定包含一个@ 2. 只能是字母数字，_- . */
  var qqReg = /^[\w\.-]+@[\w\.-]+\.[a-z\.]{2,6}/
  ```
4. 匹配url地址

  ```
    //规则：
    /*1. 以http:// https:// 开头 2. */
    var urlReg =/^https?:\/\/[\w-]+\.[a-z]{2,6}.*/
  ```
5. 身份证号
  ```
    //规则：15或18位数字 或者 17位数字＋X|x
    var identifyReg = /(^\d{15}$)|(^\d{17}[\dXx]$)/
  ```

6.  一段html代码 替换style="xxx"为空
  ```
  var styleReg = /\bstyle="[^"]*"/g
  ```
7. 把url解析成一个对象
```
// http://www.qq.com/index.html?key1=1&key2=2
/**
  {
    protocol: "http",
    hostname: "www.qq.com",
    pathname: "index.html",
    query: "key1=1&key2=2"
  }
 */
var urlReg = /^(https?):\/\/([\w-\.]+\.[a-z]{2,6})\/([\w-\.]*)\?([\w-=&]*)/g
urlReg.exec("http://www.qq.com/index.html?key1=1&key2=2")
//["http://www.qq.com/index.html?key1=1&key2=2", "http", "www.qq.com", "index.html", "key1=1&key2=2"]
```
