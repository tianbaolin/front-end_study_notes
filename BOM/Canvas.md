1. 保存canvas图片

   ```
   canvas.toDataURL('image/png')
   ```

2. canvas绘制图片

   ```javascript
   var context = document.getElementById("canvas").getContext("2d");
     //准备图片元素对象
     var img = new Image();
     img.src = "class.jpg";
     img.width = 200;
     img.height = 200;
     
     //当图片准备以后再绘制
     img.onload = function(){
         
         //绘制图片,按照图片本身的大小进行加载
        context.drawImage(img,0,0);
     }
   ```

3. Canvas 绘制dom (截屏)

   SVG `<foreignObject>`元素可以将页面上的DOM元素轻松变成图片

   ```javascript
   <svg xmlns="http://www.w3.org/2000/svg">
     <foreignObject width="120" height="50">
         <body xmlns="http://www.w3.org/1999/xhtml">
           <p>文字。</p>
         </body>
       </foreignObject>
   </svg>
   ```

   原理如下：

   1. 获取对应DOM元素的`outerHTML`代码；

   2. 放在`<foreignObject>`元素中；

   3. 图片方式显示我们的SVG图形，例如：

      ```html
      <img width="300" height="150" src='data:image/svg+xml;charset=utf-8,<svg xmlns="http://www.w3.org/2000/svg"><foreignObject width="120" height="50"><body xmlns="http://www.w3.org/1999/xhtml"><p style="font-size:12px;margin:0;">一段需要word wrap的文字。</p></body></foreignObject></svg>'>
      ```

   4. 上一步的图片本质还是SVG，我们可以借助

      ```javascript
      canvas.drawImage()
      ```

      方法将图片放在画布上，然后使用

      ```javascript
      canvas.toDataURL()
      ```

      方法转换成png或者jpg图片，核心代码：

      ```javascript
      var canvas = document.createElement('canvas');
      var context = canvas.getContext('2d');
      canvas.drawImage(img, 0, 0);
      img.src = canvas.toDataURL('image/png');
      ```