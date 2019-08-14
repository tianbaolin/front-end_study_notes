1. Event原型链

   - MouseEvent =>
   - UIEvent>
   - Event>
   - Object

2. 事件类型

   https://developer.mozilla.org/zh-CN/docs/Web/Events

   子类：

   - [`DragEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/DragEvent)
   - [`CustomEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomEvent)
   - [`MouseEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent)
   - [`KeyboardEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent)
   - [`StorageEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/StorageEvent)
   - [`TouchEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/TouchEvent)
   - [`WheelEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent)
   - [`InputEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/InputEvent)
   -  [`FocusEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/FocusEvent)
   - [`HashChangeEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/HashChangeEvent)
   - [`HashChangeEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/HashChangeEvent)

3. 属性

   * [`Event.target`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/target) 
   * [`Event.currentTarget`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/currentTarget) 
   * [`Event.deepPath`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/deepPath)

4. 方法

   * [`event.preventDefault`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/preventDefault)

     如果此事件没有被显式处理，那么它默认的动作也不要做（因为默认是要做的）。此事件还是继续传播，除非碰到事件侦听器调用[`stopPropagation()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopPropagation) 或[`stopImmediatePropagation()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopImmediatePropagation)，才停止传播。

   * [`event.stopPropagation`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopPropagation)

     阻止捕获和冒泡阶段中当前事件的进一步传播。

5. 自定义事件

   ```javascript
   app.addEventListener('click',event=>{
     console.log('event', event)
   })
   let event = new CustomEvent('click')
   app.dispatchEvent(event)
   ```

   

