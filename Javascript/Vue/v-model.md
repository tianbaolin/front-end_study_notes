



## V-Model

### 自定义输入规则

* 只有在通过规则后才允许输入的数据展示在输入框内

* 规则可以完全自定义

  ```vue 
  // handleInput 处理输入的数据
  <input type="text" v-focus v-model="content" v-on:input="handleInput" />
  // 处理输入的数据
  methods: {
      handleInput(event) {
        let value = event.target.value;
  			// 不符合规则
        if (value.length > 10) {
          this.content = this.oldContent;
        } else {
  			// 符合规则，同步历史数据
          this.oldContent = this.content;
        }
      }
    }
  ```

  ```vue
  // 手动双向绑定
  <input type="text" v-focus v-bind:value="content" v-on:input="handleInput" />
  methods: {
      handleInput(event) {
        let value = event.target.value;
  		// 先同步输入的数据
        this.content = value;
        if (value.length > 10) {
          this.content = this.oldContent;
        } else {
          this.oldContent = value;
        }
      }
    }
  ```

  