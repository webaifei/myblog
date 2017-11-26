---
title: connectjs源码解读
date: 2017-11-25 22:46:39
tags: [connect.js, node]
---
### connect基本思路
1. app.use方法入栈
	```
	var app = connect();
	// 第一个中间件
	app.use('/app', function fn1(req, res, next){
		next();
	});
	// 第二个中间件
	app.use('/app/list', function fn2(req, res, next){
		next();
	})
	// app作为接收到请求的事件函数 被调用
	http.createServer(app).listen(3000)
	```
	执行第一个中间件
	```
	var route = {
		route: '/app',
		handle: fn1
	}
	app.stack.push(route)
	```
	执行第二个中间件
	```
	var route = {
		route: '/app/list',
		handle: fn1
	}
	app.stack.push(route)
	```
2. 访问的时候 调用next出栈
	```
	//访问路径是app
	/app
	app内部调用定义的next方法
	1. 出栈添加的中间件
	2. 查看当前中间件的route是否在当前的访问路径中 继续next 直到没有可以出栈的中间件为止

	```

### 基本框架
```
var EventEmitter = require('evnets').EventEmitter;
module.exports = createServer;
var proto = {};
function createServer (){
	function app (req, res, next){
		app.handle(req, res, next);
	}
	merge(app, proto);
	merge(app, EventEmitter.prototype)
	app.stack = [];
	app.route = '/';
	return app;
}

proto = {
	use: function (route, fn){
		// 参数处理
		// code here
		this.stack.push({
			route: route, 
			handle: fn
		})
		//链式调用
		return this;
	},
	handle: function (req, res, next){
		var index = 0;
		var stack = this.stack;

	
		function next(err) {
			var layer = stack[index++];
			
			if(!layer) {
				//all done
				// code here
				return;
			}
			var route = layer.route;
			var path = parseUrl(req).pathname || '/';//获取当前请求路径
			//如果当前调用的中间件的route 和当前请求路径不匹配 则执行下一个中间件
			if(path.toLowerCase().substr(0, route.length) !== route.toLowerCase()){
				return next(err);
			}

		}
		
		next(err);
	}
}


```

TODO
1. 为啥每次修改 req.url
2. 其他容错处理