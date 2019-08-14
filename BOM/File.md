1. File 的原型链

   - File
   - Blob
   - Object

2. 通常情况下， `File` 对象是来自用户在一个 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 元素上选择文件后返回的 [`FileList`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileList) 对象,也可以是来自由拖放操作生成的 [`DataTransfer`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer) 对象，或者来自 [`HTMLCanvasElement`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement)上的 `mozGetAsFile`() API。在Gecko中，特权代码可以创建代表任何本地文件的File对象，而无需用户交互（有关详细信息，请参阅[注意事项](https://developer.mozilla.org/zh-CN/docs/Web/API/File#注意事项)。

   `File` 对象是特殊类型的 [`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)，且可以用在任意的 Blob 类型的 context 中。比如说， [`FileReader`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader), [`URL.createObjectURL()`](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL), [`createImageBitmap()`](https://developer.mozilla.org/zh-CN/docs/Web/API/ImageBitmapFactories/createImageBitmap), 及 [`XMLHttpRequest.send()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest#send()) 都能处理 `Blob` 和` File`。

3. 文件对象 转 base64

   ```javascript
   fileReader.readAsDataURL(file);
   fileReader.onload = event => {
     event.target.result
   };
   ```

   

4. 文件对象转URL

   ```javascript
   URL.createObjectURL(file)
   ```

   ```javascript
   let dom = document.getElementById("file");
   console.log("dom", dom);
   dom.addEventListener("change", event => {
     let file = event.target.files[0];
     let a = URL.createObjectURL(file);
     document.getElementById("a").src = a;
     let b = new FileReader();
     b.readAsDataURL(file);
     b.onload = event => {
       document.getElementById("b").src = event.target.result;
     };
   });
   ```

   