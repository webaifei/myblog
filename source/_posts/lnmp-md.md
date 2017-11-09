---
title: centos下搭建LNMP环境
date: 2017-11-08 13:59:55
tags: [linux, lnmp]
---

###  使用yum 安装nginx
1. 添加nginx rpm依赖包
```
rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
2. 使用yum 安装
```
yum install nginx
```
3. 启动nginx
```
service nginx start // restart stop
```

2 如果发现访问 nginx 服务 被拒绝
```
//可能是防火墙 没有允许对应的端口
firewall-cmd --list-port //查看允许的端口
//添加对应的web服务端口
firewall-cmd --add-port=80/tcp --permanent
firewall-cmd --reload
```

### yum 安装mysql
>  参考这个教程即可
http://www.cnblogs.com/julyme/p/5969626.html
TIPS:
教程中修改了mysql的密码 需要重新启动mysql服务 才能正常登陆。
### yum 安装 php
1. 源码方式安装
```
wget http://hk1.php.net/get/php-7.1.11.tar.gz/from/this/mirror
tar xzvf  php-7.1.11
./configure --prefix=/usr/local/php --enable-fpm
make
make install
```





