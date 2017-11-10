---
title: node实现命令行工具
date: 2017-11-09 19:35:51
tags: [node, 命令行]
---

### 环境变量

linux下的常见目录和作用
```
/                                             --------根目录
├── Applications                              --------mac下的程序存放目录
├── Library
├── Network
├── System
├── Users
├── Volumes
├── bin                                       --------系统命令目录 （任何用户都能执行的命令）
├── com.apple.mDNSResponder.plist.sonicwall.bk
├── cores
├── dev                                       --------硬件文件目录
├── etc -> private/etc                        --------配置文件目录
├── export
├── home                                      --------普通用户目录
├── installer.failurerequests
├── net
├── opt
├── private
├── sbin                                      --------系统命令目录 （只有root用户才能执行的命令）
├── tmp -> private/tmp
├── usr
  ├── bin                                     --------系统命令目录 （任何用户都能执行的命令）
  ├── sbin                                    --------系统命令目录 （只有root用户才能执行的命令）
└── var -> private/var
```

需要注意的文件目录：
1. bin 和 sbin 都是存放系统命令的地方 ；区别是sbin目录中的命令只有root用户才能执行
2. etc目录 是存放系统配置文件的目录， 比如hosts文件就在其中


linux 连接命令 link

```
 ln -s 软连接 (快捷方式)
 1. 拥有自己的i节点和block数据块（存储着数据 只不过存储的数据是原文件的i节点的指针）
 2. 删除了原文件的话 软连接是不能正常使用的 ；删除软连接的话 是不影响硬链接的使用的
 3. 创建软连接的话 源文件 需要指定绝对路径（如果不指定就会在当前目录下找）

 ln 硬链接 相同的i节点 相同的文件块 （可以认为是不同的指针指向同一个文件）
 1. 不能跨分区
 2. 不能针对目录

```

macOs 中添加环境变量的地方
```
1. 我们如果想在任何目录下使用我们的命令的话 就需要把我们的命令文件所在的绝对路径添加到环境变量中。
2. 和windows系统比较像，macOs中也分为系统环境变量和用户变量
3.  /etc/profile (公有的 不论哪个用户登录的 都生效)
    /etc/bashrc (公有的 不论哪个用户登录的 都生效)
    ~/.bash_profile(个人用户中的配置 建议使用)

```
如何添加
```
1. echo $PATH //查看当前的系统变量
2. 打开 ~/.bash_profile 添加如下：
# 定义一个HELLO变量
export HELLO=/Users/ngnice/projects/fe-note/node-commond-line
# 添加到$PATH中
export PATH=$HELLO:$PATH
3. 保存，退出。
4. source .bash_profile (立即生效当前的修改， 默认是每次重启登录的时候读取)
```



### 文件的权限
```
1. 执行ls -lsh
8 -rw-r--r--  1 ngnice  staff   500B  1 13 11:06 PATH
0 drwxr-xr-x  4 ngnice  staff   136B  1 13 10:34 china
8 -rw-r--r--  1 ngnice  staff    39B 11  5 20:13 file2.js
0 drwxr-xr-x  4 ngnice  staff   136B  1 26  2016 japan
0 drwxr-xr-x  5 ngnice  staff   170B  1 25  2016 nice
8 lrwxr-xr-x  1 root    staff     6B  1 13 11:47 soft-china -> china/
0 drwxr-xr-x  7 ngnice  staff   238B  5 27  2016 src
```

linux中的文件类型和权限分类
```
-rw-r--r--
上面的第一个“-”代表的是文件类型
常见的 ：
-  -》普通文件
d  -》目录文件
l  -》软连接文件
后面的9位 每三位一组 分别代表所有者，所有组，其他人权限
r 代表 read （可读权限）
w 代表 write （可写权限）
x 代表 execute （可执行权限）
```

linux 中如何修改文件（linux中一切皆文件）的权限
1. chmod u+x xxx//给xxx所有者添加可执行权限（增加）
2. chmod g-r xxx //给xxx的所有组删除可读权限（删除）
3. chmod o=rwx xxx//给xxx的其他人赋予所有权限（重新赋值）
4. chmod 755 xxx//我擦嘞，这个是啥？

> linux 中不同的权限可以使用不同的数字代表;r = 4 ,w=2,x=1;所以 chmod 755 xxx 的意思就是给xxx的所有者全部权限，给所有组读和执行权限，其他人也是读和执行权限
