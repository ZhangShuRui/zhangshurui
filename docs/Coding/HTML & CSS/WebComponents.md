## 第三方组件库

比如 Ant Design，本身是使用React写的，那么它只能在React中使用，不能在其他的框架中使用，比如Vue。

框架组件本质上最后都会通过打包工具转换成普通的HTML Tag。

### Web Components

原生支持自己的自定义标签，不用转换成基础的HTML标签，Web components使用的是[shadow dom技术](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_components/Using_shadow_DOM)。

```javascript
class MyDiv extends HTMLElement {
  constructor() {
    super();
    //open 表示可以通过页面内的 JavaScript 方法来获取 Shadow DOM，例如let myShadowDom = myCustomElem.shadowRoot;
    this.attachShadow({ mode: "open" });


    this.shadowRoot.innerHTML = /*html*/ `
        <div style='width:300px;height:300px;'>
            <slot></slot>
        </div>
    `;
  }
}
customElements.define("my-div", MyDiv);

// 第二个例子
class Counter extends HTMLElement {
  // 监听属性
  static get observedAttributes() {
    return ["count"];
  }

  attributeChangeCallback(attr, oldValue, newValue) {
    if (attr === "count") {
      this.btn.textContent = newValue;
    }
  }

  get count() {
    return this.getAttribute("count") || 0;
  }

  set count(count) {
    this.setAttribute("count", count);
  }

  constructor() {
    super();
    this.attachShadow({ mode: "open" });
    this.shadowRoot.innerHTML = /*html*/ `
          <button>${this.count}</button>
      `;

    this.btn = this.shadowRoot.querySelector("button");
    this.btn.addEventListener("click", () => {
      this.count++;
    });
  }
}
customElements.define("my-div", MyDiv);

```

渲染的结构

![[../../00 Attachment/Pasted image 20230531104946.png]]

### 原生Web Components的[生命周期回调](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_components/Using_custom_elements#using_the_lifecycle_callbacks)

定义在自定义元素的类定义中的特殊回调函数，影响其行为：
- `connectedCallback`：当自定义元素第一次被连接到文档 DOM 时被调用。
- `disconnectedCallback`：当自定义元素与文档 DOM 断开连接时被调用。
- `adoptedCallback`：当自定义元素被移动到新文档时被调用。
- `attributeChangedCallback`：当自定义元素的一个属性被增加、移除或更改时被调用。

## Web Components第三方框架-Lit.Js

Lit.js是对原生web components的封装，代码示例如下：

```javascript
import { LitElement, html, css } from "lit";
import { classMap } from "lit/directives/class-map.js";
import { styleMap } from "lit/directives/style-map.js";

class LitCounter extends LitElement {
  static properties = {
    count: {
      attribute: true,
      type: Number,
    },
    classes: {
      attribute: false,
      type: Object,
    },
    styles: {
      attribute: false,
      type: Object,
    },
  };

  static styles = [
    // 全局样式
    css`
      :host {
        display: block;
        width: 500px;
        height: 500px;
        padding: 6px;
        background-color: #ff0000;
      }
      button {
        width: 100%;
        height: 100%;
        min-width: 100px;
        min-height: 45px;
        color: var(--my-color);
      }
    `,
    // 自定义样式
    css`
      .my-text {
        font-size: 60px;
      }
    `,
  ];

  constructor() {
    super();
    this.count = 0;
    this.classes = {
      ["my-text"]: true,
    };

    this.styles = {
      cursor: "pointer",
      border: "4px solid yellow",
    };
    // 监听子元素的事件(包括slot)
    this.addEventListener("click", (e) => {
      console.log(e.type, e.target.localName);
    });
  }

  createRenderRoot() {
    const root = super.createRenderRoot();
    // 监听host事件
    root.addEventListener("click", (e) => console.log("host click!"));
    return root;
  }

  render() {
    return html`<button
      class=${classMap(this.classes)}
      style=${styleMap(this.styles)}
      @click=${{
        handleEvent: () => {
          this.count++;
        },
        // once: true,
      }}
    >
      ${this.count}
    </button>`;
  }

  async firstUpdated() {
    await new Promise(() => {
      console.log("firstUpdated");
    });

    // 首次加载完执行的回调
    // ajax请求,初始化数据
  }

  // 监听全局事件
  connectedCallback() {
    super.connectedCallback();
    window.addEventListener("resize", this._handleResize);
  }

  disconnectedCallback() {
    window.removeEventListener("resize", this._handleResize);
    super.disconnectedCallback();
  }

  _handleResize(e) {
    console.log("%c [ global event:resize ---> e ]: ", "color: blue;", e);
  }
}

customElements.define("lit-counter", LitCounter);

```



```html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    
  </head>
  <body>
    <script type="module" src="./index.js"></script>
    <lit-counter count='10'></lit-counter>
  </body>
</html>


```

## 优秀第三方Web Components库

- https://web-components.carbondesignsystem.com/?path=/story/introduction-welcome--page

- https://shoelace.style/

- https://sap.github.io/ui5-webcomponents/playground/components

- https://opensource.adobe.com/spectrum-web-components/getting-started/

- https://learn.microsoft.com/en-us/fluent-ui/web-components/

- https://kor-ui.com/introduction/welcome

- https://wiredjs.com/

- https://bendera.github.io/vscode-webview-elements/
