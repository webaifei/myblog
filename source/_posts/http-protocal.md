---
title: http协议
date: 2018-05-19 10:52:53
tags: http 计算机网络
---

### http协议
http协议是应用层协议族中的一员，是web通信基础。http协议建立在TCP（TCP是网络传输层的一个协议）协议之上。

### http报文格式
http报文分为请求报文和响应报文，报文包含了起始行、首部、实体的主题三个部分，其中起始行和首部都是ASCII文本，主体部分可以是任意数据格式的数据块。

#### 请求报文格式
1. 请求起始行：包含 请求方法、请求url、HTTP协议和版本
2. 请求首部，以key: value形式的结构
3. 空行（必须有）
4. 请求实体：任意数据组成的数据块（可以是ASCII文本或者是二进制数据等等）
```
GET /home HTTP/1.1
HOST: www.baidu.com
Connection: keep-alive
Cache-Control: max-age=100000
Cookie: xxxx=sss;


```

#### 响应报文格式
1. 响应起始行：包含 HTTP协议版本、响应状态码、原因短语
2. 响应首部：以行分割的 key: value格式
3. 响应实体
```
HTTP/1.1 200 ok
Connection: keep-alive
Cache-Control: no-cache
Content-Type: text/html
Content-Length: 1100
Set-Cookie: name=ngnice;

```

### 请求方法
GET,POST,HEAD,PUT,DELETE,OPTIONS,TRACE,
常见的是GET,POST,HEAD,OPTIONS

### 响应状态码
1. 200系列
```
200 OK
204 No Content (CORS跨域设置中针对 OPTIONS的请求有这个设置)
```
2. 300系列

|code|状态描述|含义|备注|
|----|----|----|---|
|301|Moved Permanently|永久重定向||
|302|Found|临时重定向|将来的请求还是使用老的URL|
|307|Temporary Redirect|临时重定向|将来的请求还是使用老的URL|
|304|Not Modified|协商缓存|1. 响应主体不返回内容 <br> 2. 必须是GET请求|

TIPS:
``` 
  1. 如果是重定向的code 但是没有给Location首部字段 那么响应还是之前的（因为不知道重定向到了什么地方）
  2. 302和307都是告诉浏览器请求的资源临时重定向到其他的地址了，下次请求还是请求老的地址，区别是302在HTTP/1.0中使用，307是HTTP/1.1中使用的
  3. 302和307的另外一个表现是：如果客户端发起一个POST请求，服务器返回一个302或者307 ，客户端将使用GET方法请求重定向的地址
```

3. 400系列

|code|状态描述|含义|备注|
|----|----|----|---|
|403|Forbidden|被服务器拒绝||
|404|Not Found|没有找到对应的资源||
|405|Method Not Allowed|请求的方法不支持| |
|408|Time out|超时||

4. 500系列

|code|状态描述|含义|备注|
|----|----|----|---|
|500|Internal Server Error|一般是服务器代码出错||
|404|Not Found|没有找到对应的资源||
|405|Method Not Allowed|请求的方法不支持| |
|408|Time out|超时||

### http缓存

关于http缓存header这个文章讲的不错[http缓存]