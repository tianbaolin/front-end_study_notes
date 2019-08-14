1. window的原型链

   * Window
   * WindowProperties
   * EventTarget
   * Object

2. 方法

   * *WindowTimers*(计时器)

     [`WindowTimers.clearInterval()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowTimers/clearInterval)

     [`WindowTimers.clearTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowTimers/clearTimeout)

     [`WindowTimers.setInterval()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowTimers/setInterval)

     [`WindowTimers.setTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowTimers/setTimeout)

   * *WindowBase64*(base64转码)

     [`WindowBase64.atob()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowBase64/atob)

     对 base64 编码过的字符串进行解码。

     [`WindowBase64.btoa()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowBase64/btoa)

     对一个 ASCII 编码的字符串进行 base64 编码（注意：只支持 ASCII 编码，不支持汉字）。

   * *WindowEventHandlers* (事件监听器) was 

     * [`onbeforeunload`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onbeforeunload)
     * [`onunload`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onunload)
     * [`onhashchange`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onhashchange)
     * [`onoffline`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onoffline)
     * [`ononline`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/ononline)
     * [`onpagehide`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onpagehide)
     * [`onpageshow`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onpageshow)
     * [`onpopstate`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onpopstate)
     * [`onstorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onstorage)
     * [`onunhandledrejection`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onunhandledrejection) 
     * [`onmessage`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowEventHandlers/onmessage)

   * window.open() window.close()

   * window.getComputedStyle()

   * [`Window.postMessage()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)

3. 属性

   * [`Window.console`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/console)
   * [`Window.document`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/document)
   * [`Window.history`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/history) 
   * [`Window.location`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/location)
   * [`Window.navigator`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/navigator) 
   * [`Window.performance`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/performance) 
   * [`Window.screen`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/screen) 

4. scroll

   * Window(BOM) :  scrollX(pageXOffset)、scrollY(pageYOffset)、scrollBy、scrollTo、scroll（作用和scrollTo一样）

     * ```javascript
       var x = window.scrollX;  // 以像素为单位，返回水平轴上document已经被卷去的宽度   number类型
       var y = window.scrollY;  // 以像素为单位，返回垂直方向上document被卷曲的高度     number类型
       pageYOffset 属性是 scrollY 属性的别名，pageXOffset同理，为了跨浏览器兼容，一般用后者（pageYOffset、pageXOffset）。
       ```

   * Window(BOM)：innerHeight innerWidth outerHeight outerWidth

   * Element(DOM)：scrollTo、scroll（与window一致）

   * Element(DOM)：scrollWidth、scrollHeight、scrollLeft、scrollTop 、clientHeight、 clientWidth

     

     

     <img src='./offset.png'/>

     * `scrollWidth`:只读属性，返回该元素内容区域宽度和自身宽度中较大的一个，若自身宽度大于内容宽度（存在滚动条），则scrollWidth>clientWidth.

     * ```javascript
       scrollHeight`：只读属性，返回该元素内容高度。包含被overflow隐藏掉的部分。包含padding，不包含margin.如果需要小数，请用：`Element.getBoundingClientRect().
       ```

     * 判断元素是否滚动到底部，底下等式若返回 true ，则是，否则不是

       ```javascript
       element.scrollHeight - element.scrollTop === element.clientHeight;
       ```

     * `scrollTop` 可以被设置为任何整数值，同时注意：

       - 如果一个元素不能被滚动（例如，它没有溢出，或者这个元素有一个"**non-scrollable"**属性）， `scrollTop`将被设置为`0`。
       - 设置scrollTop的值小于0，`scrollTop` 被设为`0`
       - 如果设置了超出这个容器可滚动的值, `scrollTop` 会被设为最大值.

   * Element(DOM)：offsetHeight  offsetWidth offsetParent offsetTop offsetLeft

     * **HTMLElement.offsetParent** 是一个只读属性，返回一个指向最近的（closest，指包含层级上的最近）包含该元素的定位元素。如果没有定位的元素，则 `offsetParent` 为最近的 `table`, `table cell` 或根元素（标准模式下为 `html`；quirks 模式下为 `body`）。当元素的 `style.display` 设置为 "none" 时，`offsetParent` 返回 `null`。`offsetParent` 很有用，因为 [`offsetTop`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetTop) 和 [`offsetLeft`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetLeft) 都是相对于其内边距边界的。
     * **Element.getBoundingClientRect()** 只读，返回浮点值。这个方法非常有用，常用于确定元素相对于视口的位置。该方法会返回一个DOMRect 对象，包含left, top, width, height, bottom, right六个属性：
       - `left, right, top, bottom`：都是元素（不包括margin）相对于视口的原点（视口的上边界和左边界）的距离。
       - `height, width`：元素的整体尺寸，包括被滚动隐藏的部分；padding和border参与计算。另外，`heigth=bottom-top, width=right-left`。

   

