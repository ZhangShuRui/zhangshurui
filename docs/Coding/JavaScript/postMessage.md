#postmessage

# 概念

当在Web开发中涉及多个窗口或框架之间的通信时，跨窗口通信（Cross-Window Communication）变得至关重要。`postMessage`是一种用于实现这种通信的HTML5 API，它允许不同窗口之间传递数据，即使这些窗口来自不同的域名。

`postMessage`的基本语法如下：

```javascript
otherWindow.postMessage(message, targetOrigin, [transfer]);
```

- `otherWindow`: 目标窗口的引用，可以是另一个`window`对象，如`iframe`或打开的新窗口。
- `message`: 要发送的数据，可以是字符串、对象等。
- `targetOrigin`: 指定目标窗口的源，可以是特定的域名（协议 + 域名 + 端口），也可以是通配符`*`，表示任意域名都可以接收。
- `transfer`（可选）：一个传输列表，用于将一些资源所有权从一个窗口传递给另一个窗口，通常用于传递`MessagePort`对象等。

# 示例

以下是一些使用`postMessage`进行跨窗口通信的示例：

## **示例1：父窗口与子窗口通信**

父窗口代码：

```javascript
const iframe = document.getElementById('myIframe');
const message = { text: 'Hello from parent!' };
iframe.contentWindow.postMessage(message, '*');
```

子窗口代码：

```javascript
window.addEventListener('message', event => {
  if (event.origin !== 'https://parent-domain.com') return;
  
  const receivedMessage = event.data;
  console.log(receivedMessage.text); // Output: "Hello from parent!"
});
```

## **示例2：窗口与弹出窗口通信**

主窗口代码：

```javascript
const popupWindow = window.open('popup.html', 'popup', 'width=400,height=300');
const message = 'Hello from main window!';
popupWindow.postMessage(message, '*');
```

弹出窗口代码：

```javascript
window.addEventListener('message', event => {
  if (event.origin !== 'https://main-domain.com') return;

  const receivedMessage = event.data;
  console.log(receivedMessage); // Output: "Hello from main window!"
});
```

##  **示例3：跨域的iframe通信**

在这个示例中，假设有两个不同域名的网页，它们通过一个中间页面进行通信。

中间页面代码：

```html
<!-- 中间页面位于中间域名的服务器上 -->
<script>
window.addEventListener('message', event => {
  // 验证来源，防止恶意数据传递
  if (event.origin !== 'https://origin-a.com') return;

  const receivedMessage = event.data;
  if (receivedMessage === 'get-data') {
    const data = { key: 'value' };
    event.source.postMessage(data, event.origin);
  }
});
</script>
```

页面A代码：

```javascript
const iframe = document.getElementById('iframe');
iframe.contentWindow.postMessage('get-data', 'https://middle-domain.com');
```

页面B代码：

```javascript
window.addEventListener('message', event => {
  if (event.origin !== 'https://middle-domain.com') return;

  const receivedData = event.data;
  console.log(receivedData.key); // Output: "value"
});
```

这些示例展示了如何使用`postMessage`在不同窗口之间进行跨窗口通信，无论是同域还是跨域。在实际开发中，确保进行安全验证以防止恶意数据传递非常重要。