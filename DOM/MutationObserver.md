### MutationObserver

用于监测DOM变化

1. `MutationObserver`的监听不会说同时触发多次，多次修改只会有一次回调被触发。

```javascript
const app = document.getElementById('app');
const observer = new MutationObserver(((event) => {
  console.log('event :', event);
}));
observer.observe(app, { attributes: true, childList: true, subtree: true });
app.innerText = 123;
observer.disconnect();
```

