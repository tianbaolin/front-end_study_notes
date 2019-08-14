1. 根组件

   模版：render > template > el

   ```javascript
   const app = new Vue({
     el: '#app',
     data: {
       message: 'Hello Vue!',
     },
   });
   ```

2. 组件

   * 先注册（定义组件类），再使用（实例化组件）

   * ```javascript
     // 注册组件
     Vue.component('todo-item', {
       props: ['todo'],
       template: '<li>{{todo.next}}</li>'
     });
     ```

     ```html
     <!-- 使用组件 -->
     <ol>
       <todo-item v-bind:todo="todo"></todo-item>
     </ol>
     ```

   - 组件可以指定template为模版

   - ```html
     <template id="temp">
       <tr>
         <td class="record"></td>
         <td>{{item}}</td>
       </tr>
     </template>
     ```

     ```html
     <script type="text/x-template" id="temp">
       <tr>
         <td class="record"></td>
         <td>{{item}}</td>
       </tr>
     </script>
     ```

     ```javascript
     Vue.component('todo-item', {
       props: ['todo'],
       template: '#temp',
     });
     ```

   - 组件模版插槽slot

     在模版中定位slot位置，在使用时传入slot

     ```html
     <template id="temp">
       <tr>
         <td class="record"></td>
         <td>{{item}}</td>
         <slot></slot>
       </tr>
     </template>
     ```

3. 渲染函数render

   * **渲染函数**，它比模板更接近编译器。
   * 字符串模板的代替方案，允许你发挥 JavaScript 最大的编程能力。该渲染函数接收一个 `createElement` 方法作为第一个参数用来创建 `VNode`
   * **Vue 选项中的 render 函数若存在，则 Vue 构造函数不会从 template 选项或通过 el 选项指定的挂载元素中提取出的 HTML 模板编译渲染函数**。
   * createElement，是 vue 虚拟 DOM 的概念，创建出来的并不是 html 节点，而是 **VNode**的一个类，类似 DOM 结构的一个结构，并存在内存中，它会和真正的 DOM 进行对比，若发现需要更新的 DOM，才会去转换这部分 DOM 内容，并填到真正的 DOM 中，从而**提高性能**。
   * Render 的作用 创建虚拟dom(抽象语法树，本质是js树结构对象),和真实dom 对比，若发现需要更新的 DOM，才会去转换这部分 DOM 内容，并填到真正的 DOM 中，从而**提高性能**。
   * template -> virtual DOM -> differ->real DOM

4. JavaScript 表达式（不能是语句）

   ​		模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如 `Math` 和 `Date` 。你不应该在模板表达式中试图访问用户定义的全局变量。

   ```html
   {{ number + 1 }}
   {{ ok ? 'YES' : 'NO' }}
   {{ message.split('').reverse().join('') }}
   <div v-bind:id="'list-' + id"></div>
   ```

   

5. 数据绑定

   * {{}}
   * v-bind
   * v-model

6. 指令

   * v-if
   * v-show
   * v-for
   * v-html
   * v-bind
   *  v-once 
   * v-model
   * v-on