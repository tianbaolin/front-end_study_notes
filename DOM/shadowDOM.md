### shadow dom

1. 定义

   ​		Shadow DOM它允许在文档（document）渲染时插入一棵DOM元素子树，但是这棵子树不在主DOM树中。因此无法从全局访问该dom。开发者可利用Shadow DOM 封装自己的 HTML 标签、CSS 样式和 JavaScript 代码。

2. 应用场景

   * video 标签
   * input 标签

3. 意义

   * 封装web组件内部实现机制，使其无法重外部访问和修改

4. 相关概念

   * <template>

     `<template>`元素的出现旨在让HTML模板变得更加标准与规范。

   * <content>

     通过 `<content>` 标签把来自主文档并添加到 shadow DOM 的内容被称为分布节点。

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>content&template</title>
</head>

<body>

    <div class="shadowhost">
        <em class="shadowhost_content1">唱歌</em>
        <em class="shadowhost_content2">跳舞</em>
    </div>

    <!-- S 模板标签 template -->
    <template class="template">
        <h1>你<content select=".shadowhost_content1"></content>我<content select=".shadowhost_content2"></content>!</h1>
    </template>
    <!-- E 模板标签 template -->

    <script>
    var shadowHost = document.querySelector('.shadowhost');

    var shadowRoot = shadowHost.createShadowRoot();
    var template = document.querySelector('.template');

    // template.content会返回一个文档片段，可以理解为另外一个document。
    // 利用document.importNode获取节点，true表示深度克隆。
    shadowRoot.appendChild(document.importNode(template.content, true));
    </script>

</body>

</html>
```

