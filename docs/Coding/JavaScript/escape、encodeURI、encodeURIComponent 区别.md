#js

**`encodeURI()`** 函数通过将特定字符的每个实例替换为一个、两个、三或四转义序列来对统一资源标识符 (URI) 进行编码 (该字符的 UTF-8 编码仅为四转义序列) 由两个 "代理" 字符组成)。

- 浏览器的URL接受的是ASCII编码，而ASCAII编码不包含中文和其他不在ASCAII码表中的字符，所以需要先编码成ASCAII码；

- query传参的时候，username = 'a&foo=boo' 而不用 encodeURIComponent 的话，整个参数就成了 name=a&foo=boo, 这样 CGI 就获得两个参数 name 和 foo. 这不是我们想要的

# [为什么要使用encodeURIComponent](https://www.cnblogs.com/haoqiyouyu/p/15964425.html)


