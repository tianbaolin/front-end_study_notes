### customElements

​		customElements是Window对象上的一个只读属性，接口返回一个CustomElementRegistry 对象的引用, 可以用于注册一个新的custom elements ，并且可以用于获取之前定义过的自定义元素的信息。

```javascript
customElements.define(name, constructor, options);
```

```javascript
let customElementRegistry = window.customElements;
customElementRegistry.define('my-custom-element', MyCustomElement);
```

它实际上是下列内容的简洁表示:

```
customElements.define('element-details',
  class extends HTMLElement {
    constructor() {
      super();
      const template = document
        .getElementById('element-details-template')
        .content;
      const shadowRoot = this.attachShadow({mode: 'open'})
        .appendChild(template.cloneNode(true));
  }
});
```

