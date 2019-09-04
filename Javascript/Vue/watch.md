## Watch 方法

### 1. 监听响应式数据的变化

```vue
 watch: {
    msg: {
			// 监听后立即执行，适用于props首次传入
      immediate: true,
			// 对象深度监测
      deep: true,
      handler(currentVal, oldVal) {
        console.log("currentVal :", currentVal);
        console.log("oldVal :", oldVal);
      }
    }
  }
```

### 2. 监听data, props,computed

### 3. 可以执行任何操作

### 4. 尽量使用computed替代







