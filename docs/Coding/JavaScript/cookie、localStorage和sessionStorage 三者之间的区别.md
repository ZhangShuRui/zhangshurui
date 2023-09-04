#js #前端缓存 #cookie #localStorage #sessionStorage

## 使用方式

### cookie

**保存cookie值：**

```js
    var dataCookie='110';
    document.cookie = 'token' + "=" +dataCookie; 
```

**获取指定名称的cookie值**

```js
function getCookie(name) {
  //获取指定名称的cookie值
  // (^| )name=([^;]*)(;|$),match[0]为与整个正则表达式匹配的字符串，match[i]为正则表达式捕获数组相匹配的数组；
  var arr = document.cookie.match(new RegExp("(^| )" + name + "=([^;]*)(;|$)"));
  if (arr != null) {
    console.log(arr);
    return unescape(arr[2]);
  }
  return null;
}
var cookieData = getCookie("token"); //cookie赋值给变量。
```

### localStorage | sessionStorage

localStorage和sessionStorage所使用的方法是一样的，下面以sessionStorage为例子：

```js
var name = "sessionData";
var num = 120;
sessionStorage.setItem(name, num); //存储数据
sessionStorage.setItem("value2", 119);
let dataAll = sessionStorage.valueOf(); //获取全部数据
console.log(dataAll, "获取全部数据");
var dataSession = sessionStorage.getItem(name); //获取指定键名数据
var dataSession2 = sessionStorage.sessionData; //sessionStorage是js对象，也可以使用key的方式来获取值
console.log(dataSession, dataSession2, "获取指定键名数据");
sessionStorage.removeItem(name); //删除指定键名数据
console.log(dataAll, "获取全部数据1");
sessionStorage.clear(); //清空缓存数据：localStorage.clear();
console.log(dataAll, "获取全部数据2");
```

## 三者的异同

上面的使用方式说好了，下面就唠唠三者之间的区别，这个问题其实很多大厂面试的时候也都会问到，所以可以注意一下这几个之间的区别。

### 生命周期

cookie：可设置失效时间，没有设置的话，默认关闭浏览器当前会话时候Cookie就清除了，当通过Expires或者Max-Age设置Cookie有效期时才不会自动清除；

localStorage：除非被手动清除，否则将会永久保存;

sessionStorage： 仅在当前网页会话下有效，关闭页面或浏览器后就会被清除;

### 存放数据大小：

cookie：4KB左右
localStorage和sessionStorage：可以保存5MB的信息。

### http请求：

cookie：每次都会携带在HTTP请求头中，如果使用cookie保存过多数据会带来性能问题；

```js
Cookie: name=value; name2=value2; ...
withCredentials: true // 如果要跨域的话，还需要设置这个字段
```

localStorage和sessionStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信；

### 易用性：

cookie：需要程序员自己封装，源生的Cookie接口不友好；
localStorage和sessionStorage：原生接口可以接受，亦可再次封装来对Object和Array有更好的支持；

### 其他

localStorage 和 sessionStorage 还有重要的区别：localStorage 有 **addEventListener** 方法

## 应用场景

从安全性来说，因为每次http请求都会携带cookie信息，这样无形中浪费了带宽，所以cookie应该尽可能少的使用，另外cookie还需要指定作用域，不可以跨域调用，限制比较多。但是用来识别用户登录来说，cookie还是比stprage更好用的。其他情况下，可以使用storage，就用storage。

storage在存储数据的大小上面秒杀了cookie，现在基本上很少使用cookie了，因为更大总是更好的，哈哈哈你们懂得。

localStorage和sessionStorage唯一的差别一个是永久保存在浏览器里面，一个是关闭网页就清除了信息。localStorage可以用来夸页面传递参数，sessionStorage用来保存一些临时的数据，防止用户刷新页面之后丢失了一些参数。

## 浏览器支持情况

localStorage和sessionStorage是html5才应用的新特性，可能有些浏览器并不支持，这里要注意。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/25/15ff2d54764e53af~tplv-t2oaga2asx-jj-mark:3024:0:0:0:q75.awebp)

cookie的浏览器支持没有找到，可以通过下面这段代码来判断所使用的浏览器是否支持cookie：

```js
if (navigator.cookieEnabled) {
  alert("你的浏览器支持cookie功能"); //提示浏览器支持cookie
} else {
  alert("你的浏览器不支持cookie"); //提示浏览器不支持cookie
}
```

### 数据存放处

![Cookie、localStorage、sessionStorage数据存放处](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/25/15ff2f727028f37b~tplv-t2oaga2asx-jj-mark:3024:0:0:0:q75.awebp)

Cookie、localStorage、sessionStorage数据存放处。