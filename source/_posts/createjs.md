---
title: createjs
date: 2017-11-09 19:44:13
tags: [cratejs, audio]
---
## 常见的一些问题

>  加载不同域名的图片会报跨域的错误。<br/>

### 原因是什么？

在canvas中引入了不是当前域名下的图片资源的时候， 如果我们没有设置图片的crossOrigin属性， 并且服务器端没有返回正确的头信息（Access-Control-Allow-Origin:xxx|*）的话 ，我们的canvas就会被污染（trained）,这样的结果就是我们在使用canvas中的getImageData 等操作canvas图片信息的时候会报错。根本问题是安全问题！！！

### 如何解决

设置crossOrigin属性，服务器端返回头中添加正确的头信息。
1. 默认情况下，如果我们不设置图片的这个属性的时候 就会存在trained的问题
2. 如果填写img.crossOrigin = 'anonymous' 并且服务器端能够支持这种请求，添加了相关的头信息， 那么就不会出现tained的问题 ， 我们就能正常使用了。
3. 如果填写的是img.crossOrigin = 'use-credentials' 那么服务器端那边就需要返回相关的证书
4. 如果我们填写的是除了anynomous 和use-credentials 两者之外的值 就会被当做是anonymous值来处理。


在createjs中，我们如果有操作canvas信息的方法调用就需要设置成如下
```
var loader = new createjs.LoadQueue(false, '', 'anonymous')//false
```
如果是没有那些操作就可以直接写成：
```
var loader = new createjs.LoadQueue(false)
```
>  声音播放有很多问题 需要总结 <br/>
避免： 自动播放音乐
使用 [howler.js](http://goldfirestudios.com/blog/104/howler.js-Modern-Web-Audio-JavaScript-Library) 试试



