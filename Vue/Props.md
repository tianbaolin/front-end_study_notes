## Props

### 功能：

​	父组件向子组件传递数据

* 父组件在使用子组件时传入Props

  ```vue
  <router-view :msg="'hello'" />
  ```

* 子组件在props中接受父组件传来的数据

  ```vue
  props: {
      msg: String
  },
  <h1>{{msg}}</h1>
  ```

### 特点

* props需要在子组件进行类型校验

  ```vue
   props: {
      msg: {
        type: String,
        required: false,
        default: "hello world",
        validator: msg => {
          console.log("msg", msg);
          return msg.length > 10;
        }
      }
    }
  ```

* 子组件如果不在props属性中定义接受父组件传过来的数据，父组件传递的数据会默认直接作为属性直接挂载到子组件的根元素上。但如果在子组件属性中设置```inheritAttrs:fale```则不会默认挂载

* 单向数据流

  在子组件中不能直接修改父组件传递过来的数据

