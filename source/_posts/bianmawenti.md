---
title: 前端乱码问题
date: 2017-11-09 19:37:25
tags: [乱码]
---

### 出现的原因
乱码问题 其实就是“你说的我不懂！”
> 要说清楚乱码问题 首先，需要明白http协议
http 协议简单理解就是客户端和服务端之间的一个约定。

其中的一个约定是关于传送内容的类型的： Content-Type
服务器在返回响应的时候 会指定文件的类型：Content-Type

```
//图片类型
Content-Type:image/png
//js文件
Content-Type:application/javascript;charset=UTF-8
//这个类型 兼容老得掉牙的浏览器
Content-Type:application/x-javascript

```

Content-Type字段指定文件的类型同时还能指定浏览器要使用什么字符集进行解码

同时文件在生成的时候 我们也指定了文件的编码字符集。

所以会出现下面的两种情况：
1. 服务器端指定的解码字符集和文件本身的编码字符集相同 ＝》结果：正确解析文件（没有乱码）
2. 服务器端指定的解码字符集和文件本身的编码字符集不同
  ＊ 如果解码字符集能够解析编码的字符集（类似英国人能够翻译美国人的话）文件正确解析（没有乱码）
  ＊ 指定的解码字符集不能解析编码字符集（你丫的，我听不懂！） 于是，出现了乱码问题



> 好了，问题有了，怎么解决？？？

1. 指定正确的解码字符集
2. 修改文件成服务器指定的字符集
3. 文件内容修改成能够被解码（不改变编码字符集）啊哈 这个说的有点抽象 来个栗子：

```
//js文件我们使用汉字 编码格式 utf-8
console.log('中国')
//解码字符集指定为gb2312 －》出现乱码

//修改文件内容 汉字＝》unicode
console.log('\u4e2d\u56fd') //我能行 我很行！

```

下一节，去学习怎么使用js来把汉字转换成unicode字符


> 如何使用js来把汉字转成unicode编码

```
//转换成unicode
escape(str).toLocaleLowerCase().replace(/%u/gi,'\\u');
//转换成gb2312
unescape(str.replace(/\\u/gi, '%u'));

```

这里使用了两个函数 escape 和 unescape

1.
escape 将字符转换成16进制字符串
该方法不会对 ASCII 字母和数字进行编码，也不会对下面这些 ASCII 标点符号进行编码： - _ . ! ~ * ' ( )

后面的正则替换部分，后续！！
后面的正则替换部分，后续！！


### escape encodeURI encodeURIComponent 的区别

1. escape
> * 不会对ASCII 字母和数字进行编码；
  *  不会对ASCII - _ . ! ~ * ' ( )进行编码

2. encodeURI
> * 不会对ASCII 字母和数字进行编码；
  * 不会对ASCII - _ . ! ~ * ' ( )进行编码
  * 不会对 ;/?:@&=+$,# 进行编码

3. encodeURIComponent
> * 不会对ASCII 字母和数字进行编码；
  * 不会对ASCII - _ . ! ~ * ' ( )进行编码
  * ----
  * 但是会对 ;/?:@&=+$,# 进行编码
  * 但是会对 ;/?:@&=+$,# 进行编码
  * 但是会对 ;/?:@&=+$,# 进行编码


escape 的功能和encodeURIComponent 比较相似，因为encodeURIComponent就是对uri的参数部分进行处理

> 适合的场景：
我们在url中经常需要加上某个url作为参数 ，我们在解析这个url的时候会比较麻烦，因为在参数中同时包含了一个url；
这个时候我们就可以使用 encodeURIComponent 对传入的url参数进行编码

总结：
1. escape就是对字符串进行编码，如果涉及到url就不要使用这个，
2. encodeURI 适合对整个url进行编码
3. encodeURIComponent 适合对作为参数的url进行编码

