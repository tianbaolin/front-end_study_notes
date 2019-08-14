### 1. 基本概念



1. 标记语言 元素（开始标签 结束标签 内容  属性 事件 空元素）不区分大小写，最好小写 块级元素 内联元素

2. a标签 使用 download 属性保存画布为PNG格式

```javascript
var link = document.createElement('a');
link.innerHTML = 'download image';
link.addEventListener('click', function(ev) {
    // canvas 为画布元素
    link.href = canvas.toDataURL();
    link.download = "mypainting.png";
}, false);
document.body.appendChild(link);
```

3. 实体引用

```javascript
<	&lt;
>	&gt;
"	&quot;
'	&apos;
&	&amp;
```

4. meta

在网页中指定的模式优先权高于服务器中(通过**HTTP Header**)所指定的模式。

```html
告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```

```shell
nginx
add_header "X-UA-Compatible" "IE=Edge,chrome=1";
```

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="author" content="Chris Mills">
<meta name="referrer" content="origin">
<meta name="robots" content="index">
<meta name="description" content="The MDN Learning Area aims to provide
complete beginners to the Web with all they need to know to get
started with developing web sites and applications.">
<meta http-equiv="Content-Security-Policy" content="default-src https:">
<meta http-equiv="refresh" content="60">
<meta property="og:image" content="https://developer.cdn.mozilla.net/static/img/opengraph-logo.dc4e08e2f6af.png">
```

5. head

```
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
<link rel="stylesheet" href="my-css-file.css">
<script src="my-js-file.js"></script>
<title>MDN</title>
```

6. body
   1. <i> 被用来传达传统上用斜体表达的意义：外国文字，分类名称，技术术语，一种思想……
   2. <b> 被用来传达传统上用粗体表达的意义：关键字，产品名称，引导句……
   3. <u> 被用来传达传统上用下划线表达的意义：专有名词，拼写错误……
   4. 描述列表：dl dt dd
   5. 表格：tr th td
   6. 引用：blockquote  q  cite
   7. abbr address sup sub code  var kbd samp tile
   8. figure figcaption track
   9. form datalist option pattern

7. image

   ```html
   <img srcset="elva-fairy-320w.jpg 320w,
                elva-fairy-480w.jpg 480w,
                elva-fairy-800w.jpg 800w"
        sizes="(max-width: 320px) 280px,
               (max-width: 480px) 440px,
               800px"
        src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
   ```

8. 自动补全

   ```html
   <label for="myFruit">What's your favorite fruit?</label>
   <input type="text" name="myFruit" id="myFruit" list="mySuggestion">
   <datalist id="mySuggestion">
     <option>Apple</option>
     <option>Banana</option>
     <option>Blackberry</option>
     <option>Blueberry</option>
     <option>Lemon</option>
     <option>Lychee</option>
     <option>Peach</option>
     <option>Pear</option>
   </datalist>
   ```


