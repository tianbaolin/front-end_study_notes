## Slot

### 1. 基本用法

```vue
// 父组件
<navigation-link url="/profile">
  Your Profile
</navigation-link>
```

```vue
// 子组件
<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>
```

###2. 后备内容

```vue
//子
<button type="submit">
  <slot>Submit</slot>
</button>
```

```vue
// 父
<submit-button></submit-button>
```

### 3. 具名插槽

```vue
// 子
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

```vue
// 父
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>
  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

### 4.作用域插槽

子组件向父组件插槽传递数据

**插槽 prop 允许我们将插槽转换为可复用的模板，这些模板可以基于输入的 prop 渲染出不同的内容。**这在设计封装数据逻辑同时允许父级组件自定义部分布局的可复用组件时是最有用的。

```vue
// 子组件插槽绑定user作为props
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>
```

```vue
// 父组件接收props
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

### 5. 动态插槽

```vue
<base-layout>
  <template v-slot:[dynamicSlotName]>
    ...
  </template>
</base-layout>
```

