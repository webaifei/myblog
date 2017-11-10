---
title: vituralbox 下 配置centos网络
date: 2017-11-08 14:02:14
tags: [linux, 网络]
---

### 遇到的问题
1. 没有ifconfig 命令
> 通过yum install net-tools安装
2. 没有网络
```
 可能网卡没有启动 service network restart，
 设置开机自动启动
vi /etc/sysconfig/network-scripts/ifconfig-xxx
ONBOOT=NO //改成YES
```
3. 虚拟机配置的是动态ip  和本地ip不在一个网段
```
将虚拟机网络设置 改成 “桥接网卡”
重新启动 试试
```
4、 本机 ssh 连接虚拟机 提示 22端口 refused
```
一般是因为 虚拟主机 防火墙 限制导致的
centos7防火墙使用的是 firewall
//使用如下命令添加访问权限
firewall-cmd --permanent --add-port=22/tcp
firewall-cmd --reload //更新配置
重新启动一个窗口 ssh连接（注意 如果还是在之前的窗口 可能一直不好使 ）
```

