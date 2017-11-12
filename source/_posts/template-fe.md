---
title: 前端模板实现
date: 2017-11-11 22:39:09
tags: [javascript, 前端模板]
---

> 一步一步实现自己的前端模板

最终的调用方法：
```
function template(string, data){
	//code here	
}

var str = 'this is the {{name}}';
template(str, {
	name: 'allo'
})
```

如何实现变量替换呢? 这里用到了两个正则方法
1. replace  方法返回一个由替换值替换一些或所有匹配的模式后的新字符串 (不会影响原来字符串)

2. exec 在一个指定字符串中执行一个搜索匹配。返回一个数据或者null 
```
var varReg =/\{\{([^\}]+)?\}\}/g;
//varReg.lastIndex 标记了下一次开始检索的位置 
varReg.exec(str)
[
	'{{name}}',
	'name',
	index: 22,
	input: 'this is the {{name}}'
]
```
3. 遍历所有的匹配项 进行替换
```
function template(str, data){
	var varReg = /\{\{([a-zA-Z_\$])+\}\}/g;
	var tpl = '';
	while( match = varReg.exec(str) ) {
		var replaceStr = match[0],
			replaceKey = match[1];
			tpl = str.replace(replaceStr, data[replaceKey]);
	}
	return tpl;	
}
```
4. 上面的代码有些问题，并不能支持如下的情况
```
var data = {
	info: {
		title:'title here'
	}
}
var str = 'this is the {{info.title}}';
使用上面的函数执行 {{info.title}} 将不会被替换
str.replace(str, data[info.title]);// 
```
5. 
