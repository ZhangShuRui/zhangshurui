#input #vue 
# 对Data中对象的属性劫持
![[/00 Attachment/Pasted image 20230806165616.png]]
![[/00 Attachment/Pasted image 20230806170543.png]]

![[/00 Attachment/Pasted image 20230806171426.png]]
![[/00 Attachment/Pasted image 20230806171436.png]]
![[/00 Attachment/Pasted image 20230806171517.png]]

![[/00 Attachment/Pasted image 20230806171447.png]]

递归深层代理
![[/00 Attachment/Pasted image 20230806171858.png]]
![[/00 Attachment/Pasted image 20230806172025.png]]

# 数组劫持使用方法函数劫持

![[/00 Attachment/Pasted image 20230806172139.png]]





![[/00 Attachment/Pasted image 20230806173248.png]]

![[/00 Attachment/Pasted image 20230806173712.png]]


![[/00 Attachment/Pasted image 20230806173555.png]]

![[/00 Attachment/Pasted image 20230806173921.png]]



# 实现对data中数组的对象以及添加对象进行劫持
![[/00 Attachment/Pasted image 20230806181526.png]]

![[/00 Attachment/Pasted image 20230806181605.png]]

对push追加的数据劫持
给每一个数据Value上挂载 observer 实例，方便调用observer上的方法

![[/00 Attachment/Pasted image 20230806182416.png]]

调用oberver上的方法进行劫持
![[/00 Attachment/Pasted image 20230806183009.png]]
![[/00 Attachment/Pasted image 20230806182833.png]]

# 将data上所有的属性代理到实例上

直接从vm上获取数据

![[/00 Attachment/Pasted image 20230806183443.png]]
![[/00 Attachment/Pasted image 20230806183553.png]]

# 获取到html

vue初次渲染流程：
 先初始化数据，将模板编译, 变成render() ，生成VNode，变成真实的DOM，放到页面

vue 模板编译：  template  render  el（必须要有）render()
先 render ，在template，最后el(必须)

![[/00 Attachment/Pasted image 20230806190009.png]]

![[/00 Attachment/Pasted image 20230806191643.png]]
![[/00 Attachment/Pasted image 20230806191743.png]]

# 真实DOM变为AST语法树（模板编译的过程）
![[/00 Attachment/Pasted image 20230806192159.png]]

# 创建AST语法树
（这边就是把 一段HTML字符串变成一个描述该HTML结构的对象）

![[/00 Attachment/Pasted image 20230806192302.png]]

![[/00 Attachment/Pasted image 20230806192633.png]]

![[/00 Attachment/Pasted image 20230806192906.png]]


# 将AST语法书转换render函数


HTML -> AST

![[/00 Attachment/Pasted image 20230806194530.png]]

AST -->render字符串 --->  render函数
![[/00 Attachment/Pasted image 20230806195013.png]]
![[/00 Attachment/Pasted image 20230806195516.png]]

render code字符串 --> 函数
![[/00 Attachment/Pasted image 20230806195852.png]]

![[/00 Attachment/Pasted image 20230806195834.png]]

# 将render函数变为虚拟DOM

![[/00 Attachment/Pasted image 20230806200855.png]]
![[/00 Attachment/Pasted image 20230806201259.png]]
![[/00 Attachment/Pasted image 20230806201312.png]]

![[/00 Attachment/Pasted image 20230806201613.png]]

![[/00 Attachment/Pasted image 20230806202259.png]]

大体流程：生成的render函数中，有许多的_c,   _ v,函数，这些主要就是生成VNode结构，并且将模板中的变量名替换成对应的值。

# 将虚拟DOM变成真实的DOM

![[/00 Attachment/Pasted image 20230806203123.png]]
![[/00 Attachment/Pasted image 20230806203200.png]]

将生成的真实的DOM替换旧的DOM
![[/00 Attachment/Pasted image 20230806203356.png]]

![[/00 Attachment/Pasted image 20230806203438.png]]

![[/00 Attachment/Pasted image 20230806203428.png]]

自此，原来的模板HTML 变成了 带有数据的新HTML

面试题：
Vue渲染流程：
数据初始化 --> 模板编译 ---> render函数（ast -> render字符串 --> render函数）---> vnode --> 内存中真实DOM --> 替换旧的DOM

# 使用策略模式合并生成生命周期

![[/00 Attachment/Pasted image 20230806211652.png]]
![[/00 Attachment/Pasted image 20230806211715.png]]

![[/00 Attachment/Pasted image 20230806211825.png]]

# 实现Dep（依赖收集）
[# Vue响应式原理-理解Observer、Dep、Watcher](https://juejin.cn/post/6844903858850758670)
[彻底理解Vue中的Watcher、Observer、Dep](https://juejin.cn/post/6844903901003513863?searchId=202308071027514A4F9139F0C28FC0A573)

![[/00 Attachment/Pasted image 20230807102017.png]]
![[/00 Attachment/Pasted image 20230807102717.png]]
![[/00 Attachment/Pasted image 20230807102725.png]]

新建dep.js
![[/00 Attachment/Pasted image 20230807103755.png]]

![[/00 Attachment/Pasted image 20230807103910.png]]

个人总结：
- Observer会把data中的数据进行数据劫持（Object.definedProperty）
- new Watch(),new Watch()的构造器中，把当前Watch实例this赋值到Depend.target(Depend.target = this),然后调用访问当前数据，触发get方法，
触发Dep.depend(),然后当前watcher就被加到dep实例下面的subs数组中。完成依赖的收集。
- 同样的，set() 触发notify（）。执行watcher中的方法

以上以利用了发布订阅的设计模式。

# diff 算法

[[03 Coding/VueJS/Vue diff 算法.canvas|Vue diff 算法白板]]


https://www.bilibili.com/video/BV1JR4y1R7Ln/?spm_id_from=..search-card.all.click&vd_source=633fb585b48e246e65d0f363285629b9

![[/00 Attachment/Pasted image 20230807111338.png]]


![[/00 Attachment/Pasted image 20230807111358.png]]


![[/00 Attachment/Pasted image 20230807111418.png]]

本质，比较2个JS对象
 ![[/00 Attachment/Pasted image 20230807111512.png]]
 ![[/00 Attachment/Pasted image 20230807112035.png]]

 ![[/00 Attachment/Pasted image 20230807112119.png]]

 比对子节点

 同级比对
 ![[/00 Attachment/Pasted image 20230807112150.png]]
 ![[/00 Attachment/Pasted image 20230807112229.png]]
 

 **尚硅谷的关于diff算法的课程**
 https://www.bilibili.com/video/BV1v5411H7gZ/?spm_id_from=..search-card.all.click&vd_source=633fb585b48e246e65d0f363285629b9
 
 ![[/00 Attachment/Pasted image 20230807133542.png]]

 ![[/00 Attachment/Pasted image 20230807133730.png]]

 ![[/00 Attachment/Pasted image 20230807133808.png]]

 ![[/00 Attachment/Pasted image 20230807133831.png]]

 ![[/00 Attachment/Pasted image 20230807133921.png]]

 ![[/00 Attachment/Pasted image 20230807133951.png]]

 ![[/00 Attachment/Pasted image 20230807134045.png]]

 ![[/00 Attachment/Pasted image 20230807170637.png]]
![[/00 Attachment/Pasted image 20230807172158.png]]


配置webpack,注意这里使用webpack5
 ![[/00 Attachment/Pasted image 20230807170832.png]]
![[/00 Attachment/Pasted image 20230807170920.png]]
![[/00 Attachment/Pasted image 20230807171228.png]]

 官方给的Demo例子
 ![[/00 Attachment/Pasted image 20230807172005.png]]

 注意这里要使用webpack5
 ![[/00 Attachment/Pasted image 20230807172053.png]]

 虚拟DOM与h函数
 ![[/00 Attachment/Pasted image 20230807172324.png]]

![[/00 Attachment/Pasted image 20230807172558.png]]

![[/00 Attachment/Pasted image 20230807172951.png]]

![[/00 Attachment/Pasted image 20230807173112.png]]
![[/00 Attachment/Pasted image 20230807173205.png]]
 ![[/00 Attachment/Pasted image 20230807173359.png]]
![[/00 Attachment/Pasted image 20230807173537.png]]
 ![[/00 Attachment/Pasted image 20230807173632.png]]

  ![[/00 Attachment/Pasted image 20230807214352.png]]

  ![[/00 Attachment/Pasted image 20230807214434.png]]

 ![[/00 Attachment/Pasted image 20230807214830.png]]

 ## 手写h函数

vnode.js文件
 ![[/00 Attachment/Pasted image 20230807221034.png]]
h.js 
 ![[/00 Attachment/Pasted image 20230807221456.png]]
![[/00 Attachment/Pasted image 20230807222059.png]]

![[/00 Attachment/Pasted image 20230809203036.png]]

![[/00 Attachment/Pasted image 20230809203420.png]]
## 感受diff算法

![[/00 Attachment/Pasted image 20230809204013.png]]

patch 函数是diff算法的核心函数
![[/00 Attachment/Pasted image 20230809204232.png]]

![[/00 Attachment/Pasted image 20230809204442.png]]
![[/00 Attachment/Pasted image 20230809204922.png]]

![[/00 Attachment/Pasted image 20230809205216.png]]

Vue 如何判断是相同的节点：**选择器相同且Key相同**

![[/00 Attachment/Pasted image 20230809205540.png]]
![[/00 Attachment/Pasted image 20230809205739.png]]

**只会同层比较，不会跨层比较**
![[/00 Attachment/Pasted image 20230809205900.png]]

> 一般很少在实际的项目中，会出现在一组dom节点外，动态添加一层标签的情况。

## diff处理新旧节点不是同一个节点时
![[/00 Attachment/Pasted image 20230809211924.png]]

大体的比较流程
![[/00 Attachment/Pasted image 20230809211933.png]]

如何定义“同一个节点”？
答案：选择器和Key相同
![[/00 Attachment/Pasted image 20230809212037.png]]

## 手写第一次上树时

目标：第一次patch函数被调用时
![[/00 Attachment/Pasted image 20230809214550.png]]
- 判断旧节点是虚拟节点还是真实的DOM节点，如果是真实的节点就转换成VNode；
![[/00 Attachment/Pasted image 20230809213032.png]]

- 判断是不是相同的节点
![[/00 Attachment/Pasted image 20230809213331.png]]

创建一个createElement.js,用来创建真正的DOM节点并插入页面
![[/00 Attachment/Pasted image 20230809213534.png]]

 ![[/00 Attachment/Pasted image 20230809214158.png]]

## 手写递归创建子节点

![[/00 Attachment/Pasted image 20230809214308.png]]

 
![[/00 Attachment/Pasted image 20230809214901.png]]
![[/00 Attachment/Pasted image 20230809215208.png]]

![[/00 Attachment/Pasted image 20230809215527.png]]
最后还需要把老节点删除
![[/00 Attachment/Pasted image 20230810112017.png]]

![[/00 Attachment/Pasted image 20230810112154.png]]

## diff处理新旧节点是相同的的节点

![[/00 Attachment/Pasted image 20230810113118.png]]

vnode1、vnode2 是相同的节点，那么什么都不用做。
![[/00 Attachment/Pasted image 20230810114003.png]]


## 手写新旧节点text不同的情况

判断新旧vnode是不是同一个节点，如果相等就什么不用做；
新vnode有没有text（没有children）

新vnode有子节点children，父节点没有子节点children（有text）的情况下：

![[/00 Attachment/Pasted image 20230810135639.png]]

最复杂的情况是：新旧节点都有子节点

## 尝试书写diff更新子节点
![[/00 Attachment/Pasted image 20230810141601.png]]

把data中的Key拿出来

![[/00 Attachment/Pasted image 20230810154510.png]]

子节点 ABC ---> ABCD 
![[/00 Attachment/Pasted image 20230810154555.png]]
![[/00 Attachment/Pasted image 20230810154756.png]]

![[/00 Attachment/Pasted image 20230810155012.png]]


算法很差，抛弃
![[/00 Attachment/Pasted image 20230810160750.png]]
## diff算法的子节点更新策略（重点）

![[/00 Attachment/Pasted image 20230810164642.png]]

![[/00 Attachment/Pasted image 20230810165047.png]]
![[/00 Attachment/Pasted image 20230810165432.png]]
![[/00 Attachment/Pasted image 20230810165643.png]]
![[/00 Attachment/Pasted image 20230810171432.png]]
![[/00 Attachment/Pasted image 20230810172133.png]]

![[/00 Attachment/Pasted image 20230810172149.png]]

## 手写diff算法子节点更新策略

![[/00 Attachment/Pasted image 20230810172414.png]]

![[/00 Attachment/Pasted image 20230810173237.png]]

![[/00 Attachment/Pasted image 20230810173119.png]]

![[/00 Attachment/Pasted image 20230810173605.png]]

## 动画演示diff算法过程
[动画演示](https://www.bilibili.com/video/BV1b5411V7i3/?spm_id_from=333.337.search-card.all.click)
