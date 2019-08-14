1. EventTarget=原型链

   - EventTarget=>
   - Object

2. EventTarget`是一个由可以接收事件的对象实现的接口，并且可以为它们创建侦听器。

3. 在讨论各种监听事件的方法时：

   -  **事件侦听器（event listener）**是指通过 [`EventTarget.addEventListener()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener) 注册的函数或对象,
   - **事件处理器（event handler）**是指通过 `on...`  属性注册的函数。

4. 方法

   - [`EventTarget.addEventListener()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)

     在EventTarget上注册特定事件类型的事件处理程序。

   - [`EventTarget.removeEventListener()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/removeEventListener)

     EventTarget中删除事件侦听器。

   - [`EventTarget.dispatchEvent()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/dispatchEvent)

     将事件分派到此EventTarget。

   

   

   

   

   

   

