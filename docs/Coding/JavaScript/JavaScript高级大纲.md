#js
# 深入JavaScript高级语法

## 一. JavaScript运行环境

### 1. 浏览器工作原理

- 浏览器内核
- 渲染引擎工作原理
- WebKit内核

	- WebCore
	- JavaScriptCore

### 2. v8引擎工作原理

- JavaScript引擎

	- SpiderMonkey
	- Chakra
	- JavaScriptCore
	- V8引擎

- V8引擎工作原理

	- Parse：转换器
	- Ignition：解释器
	- TurboFan：编译器
	- Orinoco：垃圾回收

### 3. JavaScript内存管理

- 理解内存管理

	- 什么是内存管理
	- 手动管理内存

- 常见的GC内存算法

	- JavaScript的垃圾回收（Garbage Collection）
	- 引用计数算法
	- 标记清除算法
	- 标记整理算法
	- 分代回收算法

- V8引擎内存管理

	- V8的分代算法
	- V8内存的分配
	- 新生代对象回收
	- 旧生代对象回收

- Performance调试
- JavaScript内存泄露

### 4. JavaScript事件循环

- 浏览器的进程模式

	- 线程
	- 进程
	- JavaScript线程

- 浏览器的事件循环

	- 宏任务macrotask
	- 微任务microtask
	- 常见的面试题

- Node的事件循环

	- libuv
	- 阻塞IO
	- 非阻塞IO
	- 宏任务macrotask
	- 微任务microtask
	- 常见的面试题

## 二. JavaScript作用域和函数

### 1. 认识作用域

- 认识作用域

	- JavaScript编译和执行
	- 深入理解作用域
	- 作用域的嵌套

- 词法作用域

	- 认识词法分析
	- eval函数
	- with关键字

- 作用域提升

	- JavaScript疑惑面试题分析
	- 编译器中的变量声明和提升
	- 函数和变量的提升

- 块级作用域

	- with作用域
	- try...catch...作用域
	- let变量声明
	- const变量声明

- 作用域相关的面试题

### 2. 执行上下文

- 执行上下文

	- Global EC
	- Function EC
	- Eval EC

- 变量对象VO

	- VO(G)全局变量对象
	- AO(Active Object)私有变量对象
	- GO(Global Object)全局对象

### 3. 深入函数执行

- call/apply执行函数
- 立即执行函数
- Scopechain

	- 函数的生命周期

		- 定义
		- 调用时
		- 调用后

	- 函数执行过程的作用域链
	- 作用域链面试题

- 深入闭包

	- 为什么需要闭包
	- 闭包的访问规则
	- 闭包的应用场景
	- 闭包的注意事项
	- 闭包相关的面试题

### 4. 函数的this绑定

- this指向什么

	- 为什么使用this
	- this指向什么

- this绑定规则

	- 默认绑定
	- 隐式绑定
	- 显示绑定

		- call/apply/bind
		- 内置函数

	- new绑定

- 绑定的优先级

	- 默认绑定的优先级最低
	- 显示绑定优先级高于隐式绑定
	- new绑定优先级高于隐式绑定
	- new绑定优先级高于bind

- 绑定之外this

	- 忽略显示绑定
	- 间接函数引用
	- ES6箭头函数

- this相关的面试题

### 5. 函数的柯里化

- 认识柯里化

	- 什么是柯里化（Currying）
	- 柯里化有什么作用？

- 实现柯里化

	- 案例代码改造
	- 柯里化的实现

- 柯里化应用

	- 柯里化应用场景

## 三. JavaScript面向对象

### 1. 深入理解对象

- 对象的语法

	- 对象字面量
	- 对象的类型
	- 函数对象

- 对象的内容

	- 属性和方法定义
	- 对象属性描述符

		- [[Configurable]]
		-  [[Enumerable]]
		- [[Writable]]
		- [[Value]]
		- [[Get]]
		- [[Set]]

	- 访问器属性使用

		- Object.defineProperty
		- Object.defineProperties
		- Object.getOwnPropertyDescriptor

	- 对象的属性判断

		- hasOwnProperty
		- in关键字
		- for..in..
		- for..of..

- 对象的拷贝

	- 对象的引用赋值
	- 对象的浅拷贝
	- 对象的深拷贝

- ES6对象增强

	- Object.is()
	- 简写属性名
	- 可计算属性名称
	- 简写方法名
	- 对象的解构

		- 嵌套解构
		- 部分解构
		- 参数上下文匹配

### 2. 面向对象编程

- 理解面向对象

	- 什么是面向对象编程？
	- 面向对象编程的特性

		- 封装
		- 继承
		- 多态

	- 类和对象的关系

- 创建对象方式

	- 工厂模式创建
	- 构造函数模式
	- 原型创建模式

		- 认识原型
		- prototype 属性
		- constructor 的属性
		- __proto__属性

- 面向对象继承

	- 认识原型链

		- 深入原型对象
		- 简洁的原型语法
		- 修改原型的属性
		- 深入理解原型链
		- 原型和实例的关系
		- 原型链存在的问题

	- 继承的实现

		- 经典继承

			- 实现方式
			- 存在弊端

		- 组合继承

			- 实现方式
			- 存在弊端

		- 原型式继承

			- 实现方式
			- 存在弊端

		- 寄生式继承

			- 实现方式
			- 存在弊端

		- 集成式组合继承

			- 释放方式

- ES6类的使用

	- class类的定义

		- 构造方法
		- 属性定义
		- 方法定义

	- 类的实例化过程

		- 类的构建过程解析
		- 类的类型

			- function类型

	- 属性分类解析

		- 实例属性和方法
		- 原型属性和访问器
		- static类方法和属性

	- class类的继承

		- extends关键字
		- super函数的使用

			- 构造函数
			- 普通函数

	- Babel的处理

		- Babel工具对class的处理

			- 阅读Babel转换后的代码

		- Babel对继承的转换处理

			- Babel继承的源码阅读
			- _inherits
			- _possibleConstructorReturn
			- _classCallCheck

- 面向对象面试题

## 四. ES6~12新特性讲解

### 1.新特性查询

- https://ecmascriptfeatures.online/

### 2. ES6常见新特性

- 新类型

	- Symbol
	- Promise
	- Reflect
	- Proxy
	- WeakSet
	- WeakMap
	- Set
	- Map

- 新特性

	- generators
	- class
	- arrow functions
	- template string literals
	- for...of
	- enhanced object literals
	- spread syntax
	- rest parameter
	- default function parameters

### 3. ES7常见新特性

- 新特性

	- Array.prototype.includes()

### 4. ES8常见新特性

- 新特性

	- rest/spread properties
	- await
	- async

### 5. ES9常见新特性

- 新特性

	- Promise.prototype.finally()
	- rest/spread properties
	- asynchronous generators and iteration

### 6. ES10常见新特性

- 新特性

	- Array.sort()
	- catch without argument

### 7. ES11常见新特性

- 新特性

	- import.meta
	- module namespace exports
	- globalThis
	- optional chaining syntax
	- nullish coalescing operator ??
	- dynamic import

### 8. ES12常见新特性

- 新特性

	- Promise.any
	- logical assignment operators: &&=, ||=, ??=

## 五. JavaScript异步处理

### 1. 迭代器和生成器

- 深入迭代器

	- 认识迭代器

		- 什么是迭代器
		- 什么是迭代器模式

	- 可迭代类型

		- 字符串String
		- 数组Array
		- 映射Map
		- 集合Set
		- arguments对象
		- 等等...

	- 迭代类型操作

		- for-of 循环
		- 数组解构
		- 扩展操作符
		-  yield*操作符，在生成器中使用
		- 等等...

	- 迭代器协议

		- Symbol.iterator
		- iter.next

	- 自定义迭代器

		- 实现Symbol.iterator
		- 实现next

	- 终止迭代器

		- break、continue、return、throw
		- 结构操作值消耗

- 深入生成器

	- 认识生成器

		- 什么是生成器
		- 生成器的作用

	- 生成器函数

		- 创建生成器函数
		- 生成器函数的调用

	- yield关键字

		- yield中断执行
		- yield输入和输出
		- 生成可迭代对象

	- 生成器和迭代器
	- 终止生成器

		- return()
		- throw()

### 2. Promise的使用

- 异步代码处理

	- 代码执行的顺序
	- 异步代码执行
	- 事件循环
	- 并行和并发执行
	- 函数的回调

- Promise的API

	- 认识Promise

		- Promises/A+规范
		- Promise的状态

			- 待定(pending)
			- 完成(fulfilled)
			- 拒绝(rejected)

	- 创建Promise

		- Promise构造器

			- resolve
			- reject

		- Promise.resolve()
		- Promise.reject()
		- Promise.all([ .. ])
		- Promise.race([ .. ])

	- Promise的处理

		- then
		- catch
		- finally

	- Promise链式

### 3. async和await

- async、await基础

	- 和Promise的关系
	- await
	- async

- 和generator的关系
- async、await优缺点

## 六. 模块化和包管理工具

### 1. JS模块化开发

- 认识模块化开发

	- JavaScript设计缺陷
	- 没有模块化带来的问题

- CommonJS规范

	- CommonJS和Node的区别和关系
	- exports导出
	- module.exports导出
	- require导入和细节
	- 模块的加载顺序

- AMD和CMD规范

	- CommonJS规范缺点
	- AMD规范

		- require.js
		- require.config
		- require
		- define

	- CMD规范

		- SeaJS
		- define
		- require
		- exports
		- module

- ESModule模块化

	- export关键字
	- import关键字
	- export和import结合
	- default用法
	- import()异步导入

- ES Module和CommonJS

	- ES Module和CommonJS的区别
	- ES Module和CommonJS的交互

### 2. npm包管理工具

- 认识npm工具
- package.json

	- 必须填写的属性：name、version
	- private属性
	- main属性
	- scripts属性
	- dependencies属性
	- devDependencies属性
	- engines属性
	- browserslist属性

- 版本管理的问题

	- semver版本规范

		- X主版本号（major）
		- Y次版本号（minor
		- Z修订号（patch

	- ^x.y.z
	- ~x.y.z

- npm install解析

	- npm install命令

		- 全局和局部安装

	- npm install原理

		- package-lock.json
		- 查找规则
		- 查找缓存
		- 等等...

	- npm其他常见命令

- 其他工具对比

	- yarn
	- cnpm
	- npx

## 七. JavaScript特性补充

### 1. Proxy和Reflect

- Proxy

	- 认识proxy

		- Proxy的作用
		- Proxy应用场景

	- 处理方法

		- get
		- set
		- has
		- deleteProperty
		- apply
		- construct
		- getPrototypeOf
		- setPrototypeOf
		- ownKeys
		- 等等...

	- 处理参数

		- target
		- property
		- value
		- receiver

- Reflect

	- 认识Reflect

		- Reflect的作用
		- Reflect应用场景

	- 处理方法

		- get
		- set
		- has
		- deleteProperty
		- apply
		- construct
		- getPrototypeOf
		- setPrototypeOf
		- ownKeys
		- 等等...

	- 处理参数

		- target
		- property
		- value
		- receiver

### 2. JSON的序列化

- JSON表示形式

	- 简单值
	- 对象
	- 数组

- JSON的序列化

	- JSON.stringify

		- 使用
		- 参数

			- 过滤器
			- 字符串缩进

		- toJSON方法

	- JSON.parse

		- 使用

### 3. 浏览器API操作

-  浏览器BOM操作

	- window对象
	- location对象
	- history对象

- 2. 浏览器DOM操作

	- Node节点类型
	- DOM的元素操作
	- DOM的样式操作

- 3. 浏览器事件处理

	- 事件冒泡
	- 事件捕获
	- DOM事件流
	- 事件对象
	- 常见事件类型

- 4. 浏览器存储方案

	- cookie
	- localStorage
	- sessionStorage

## 八. 手写工具案例练习

### 1. 节流函数的实现

- 认识防抖函数
- 防抖的三方库

	- lodash
	- underscore

- 手写防抖函数

	- 防抖基本功能
	- 优化的参数
	- 绑定this
	- 优化取消功能
	- 优化立即执行
	- 优化返回值

### 2. 防抖函数的实现

- 认识节流函数
- 节流的三方库

	- lodash
	- underscore

- 手写节流函数

	- 节流基本功能
	- 优化参数和this
	- 优化最后执行功能
	- 优化取消功能
	- 优化返回值

### 3. 实现深拷贝案例

- 认识深拷贝
- 拷贝的三方库

	- lodash
	- underscore

- 手写深拷贝函数

	- 深拷贝基本功能
	- 递归拷贝功能
	- 不同类型的处理
	- 函数的拷贝功能

