#JS #事件循环

https://www.bilibili.com/video/BV1GV411s7G6?p=2&vd_source=633fb585b48e246e65d0f363285629b9

## 浏览器有哪些线程

![[../../00 Attachment/Pasted image 20230804140208.png]]
![[../../00 Attachment/Pasted image 20230804140330.png]]
![[../../00 Attachment/Pasted image 20230804140400.png]]
![[../../00 Attachment/Pasted image 20230804140412.png]]
**先同后异，先微后宏，大的原则**
![[../../00 Attachment/Pasted image 20230804142314.png]]


![[../../00 Attachment/Pasted image 20230804141123.png]]

Promise里面的代码是同步代码，只有遇到 resolve   reject 的时候才会执行异步代码
![[../../00 Attachment/Pasted image 20230804141357.png]]

await、async 本意就是用同步函数的语法糖表示异步
如何async没有用到await就是普通的函数。

![[../../00 Attachment/Pasted image 20230804142556.png]]

![[../../00 Attachment/Pasted image 20230804142851.png]]
![[../../00 Attachment/Pasted image 20230804143003.png]]

![[../../00 Attachment/Pasted image 20230804144435.png]]

![[../../00 Attachment/Pasted image 20230804145522.png]]

## 微任务和宏任务[​](https://www.1024nav.com/front-junior/browser-basic#%E5%BE%AE%E4%BB%BB%E5%8A%A1%E5%92%8C%E5%AE%8F%E4%BB%BB%E5%8A%A1)

### 宏任务[​](https://www.1024nav.com/front-junior/browser-basic#%E5%AE%8F%E4%BB%BB%E5%8A%A1 "Direct link to heading")

宏任务一般是由浏览器发起的，比如SCRIPT代码，异步请求（ajax请求），事件回调，定时器等。

宏任务包含

```
script(整体代码)
setTimeout
setInterval
I/O
UI交互事件
postMessage
MessageChannel
setImmediate(Node.js 环境)
```

### 微任务[​](https://www.1024nav.com/front-junior/browser-basic#%E5%BE%AE%E4%BB%BB%E5%8A%A1 "")

微任务一般是由JS自身创建，比如 `Promise` ，`MutationObserver` ，`Object.observe` ·，`process.nextTick` 等

## 个人总结

首先要知道 await 是 promise变体，知道async函数里面没有await标注的语句是同步的语句，立马执行，await 的语句相当于new Promise()中的语句也是同步的，立马执行，而await后面的语句，相当于then()里面的语句，是异步的微任务语句，需要放进队列等待执行。js引擎，会继续往下执行其他的同步语句。