## Event

###1. 基本使用方法

```vue
// 子组件
<input type="text" v-model="input" @input="handleInput" />
 handleInput(event) {
      console.log("event", event);
      let res = this.$emit("input", event.currentTarget.value);
      console.log("res === this :", res === this);
}
```

```vue
// 父组件
<HelloWorld msg="Welcome to Your Vue.js App" @input="handle" />
```

### 2. 原生事件类型

* input
* change
* click
* submit
* scroll
* keyup
* keydown
* Focus

### 3.事件修饰符

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`
- `.passive`

### 4. 按键修饰符

* `.enter`
* `.tab`
* `.delete` (捕获“删除”和“退格”键)
* `.esc`
* `.space`
* `.up`
* `.down`
* `.left`
* `.right`

### 5. 系统修饰符

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`
- ```exact```
- ```left```
- ```right``
- ```middle```
- 