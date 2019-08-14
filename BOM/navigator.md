1. 断网检测

```javascript
window.addEventListener('offline', function () {
            console.log('offline')
        })
navigator.onLine
```

2. 有时候，特别是手机端浏览器，比如当你点击前进/后退按钮的时候，浏览器会进行缓存。但是在有些场景下，你可能不需要浏览器的这种功能。有如下解决办法：

   ```
   window.addEventListener('pageshow', (event) => {
     // 检查前进/后退缓存，是否从缓存加载页面
     if (event.persisted || window.performance && 
       window.performance.navigation.type === 2) {
       // 进行相应的逻辑处理
     }
   };
   ```

   

