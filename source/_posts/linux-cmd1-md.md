---
title: linux基础命令
date: 2017-11-08 14:01:19
tags: [linux, 命令]
---

## find 查找文件

* 注意点
find 不支持正则表达式 只支持通配符
find是完全匹配

|符号|含义|
|--|----|
| * | 匹配任意内容|
|?|匹配任意一个字符|
|[]|匹配其中的任意一个字符|

```
//查找所有的文件
find ./ -name "*"

//查找以test开头的文件和文件夹
find ./ -name test*

//查找以test结尾的文件和文件夹
find ./ -name *test
//查找包含test的文件和文件夹
find ./ -name *test*

//查找当天创建的文件和文件夹
 find ./ -ctime 0
//查找1天之内创建的文件夹和文件
find ./ -ctime -1
//查找1天之前创建的文件件和文件
find ./ ctime +1


```

## grep
grep支持正则
grep是模糊匹配（最大范围匹配）
```
//查看包含了test的行
grep test
//查看以test结尾的行
grep test$
//查看以test开头的行
grep ^test
//查看是test的行
grep ^test$
//


```

### 针对用户的操作
```
查看当前用户名
who or whoami
查看当前用户所在的用户组和组内其他成员
groups user_name
查看所有的用用户组
cat /etc/group
改变文件所属的用户组和用户名
chown groupname:username  file_name
```

