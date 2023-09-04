#vue #keep-alive #lru
## 定义

[`<KeepAlive>`](https://cn.vuejs.org/guide/built-ins/keep-alive.html) 是一个内置组件，它的功能是在多个组件间动态切换时缓存被移除的组件实例。

## 原理

核心算法：LRU（least recently used）

- 使用 LRU 缓存机制进行缓存，max 限制缓存表的最大容量
- 根据设定的 include/exclude（如果有）进行条件匹配,决定是否缓存。不匹配,直接返回组件实例
- 根据组件 ID 和 tag 生成缓存 Key ,并在缓存对象中查找是否已缓存过该组件实例。如果存在,直接取出缓存值并更新该 key 在 this.keys 中的位置(更新 key 的位置是实现 LRU 置换策略的关键)
- 获取节点名称，或者根据节点 cid 等信息拼出当前 组件名称
- 获取 keep-alive 包裹着的第一个子组件对象及其组件名

## 用法

### vue2中的用法

![[00 Attachment/Pasted image 20230813153957.png]]

以上的用法，会让所有匹配上路径的组件都会被缓存。如果我们让指定的组件被缓存，该如何做呢？

方法1：

![[00 Attachment/Pasted image 20230813154214.png]]

方法2:

![[00 Attachment/Pasted image 20230813154348.png]]

方法3：

![[00 Attachment/Pasted image 20230813154658.png]]

方法4：

![[00 Attachment/Pasted image 20230813154744.png]]

![[00 Attachment/Pasted image 20230813154804.png]]

方法5（动态组件使用keepalive）：
![[00 Attachment/Pasted image 20230813155618.png]]

### vue3中的用法

vue3中。已经不可以像vue2中直接使用keep-alive了，需要借助插槽。

![[00 Attachment/Pasted image 20230813155906.png]]

## 2个生命周期

![[00 Attachment/Pasted image 20230813160157.png]]
