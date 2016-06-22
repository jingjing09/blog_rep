---
title: webpack
date: 2016-06-22 13:06:24
tags:
---
## why

我们为什么需要 webpack？这个首先要从模块化说起。现有的模块化系统有：

1. \<script\> 标签

	这是最最原始的 js 文件加载方式， 把每一个 js 文件都看做一个模块。

	~~~javascript
	<script src="demo.js"></script>
	<script src="test.js"></script>
	~~~
	
	优点：
	
	- 简单易用
		
	缺点：
	
	 - 所有的接口变量都定义在全局作用域 *window* 下，容易引起命名冲突
	 - 模块只能按照 \<script\> 标签书写顺序进行加载
	 - 开发人员不得不去解决模块之间的依赖关系
	 - 在大型项目中，依赖关系会更加复杂以至于难以管理

	
2. CommonJS

	node.js 就是遵循 CommonJS规范，该规范通过 *require* 方法同步加载所依赖的模块，然后通过向 *exports* 添加属性或者对 *moudle.exports* 赋值来暴露接口。

	~~~javascript
	require("moudle")
	require("../file.js")
	exports.doSomething = function () {}
	moudle.exports = someValue
	~~~
	
	优点：
	
	- 简单易用
	- 便于服务端模块重用
	- 已经有很多模块遵循这种规范（npm）
	
	缺点：
	
	- 同步加载会造成阻塞
	- 不能并行加载多个模块
	
3. AMD

	AMD(Asynchronous Moudle Definition) 是 RequireJS 在推广过程中对模块定义的规范化产出。异步加载模块，推崇依赖前置，提前执行。
	
	~~~javascript
	define(id?, dependence?, factory);

	define("mymoudle", ["moudle", "../file"], function(moudle, file){
	  moudle.doSomething()
	  file.doSomething()
	  exports.action = function(){}
	})
	~~~

4. CMD

	CMD(Common Moudle Definition) 是 SeaJS 在推广过程中对模块定义的规范化产出。推崇依赖就近，延迟执行。As lazy as possible。
	
	~~~javascript
	
	~~~

5. UMD
6. ES6模块


## 安装

## Demo
