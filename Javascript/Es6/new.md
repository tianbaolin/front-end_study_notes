## new

![image-20190925134130599](/Users/tianbaolin/Library/Application Support/typora-user-images/image-20190925134130599.png)

### 1. New 过程

* 创建了一个全新的对象。
* 生成的新对象会绑定到函数调用的`this`。
* 这个对象会被执行`[[Prototype]]`（也就是`__proto__`）链接。
* 如果函数没有返回对象类型`Object`(包含`Functoin`, `Array`, `Date`, `RegExg`, `Error`)，那么`new`表达式中的函数调用会自动返回这个新的对象。

```javascript
function create(Con, ...args) {
  let obj = {}
  let result = Con.apply(obj, args)
  Object.setPrototypeOf(obj, Con.prototype)
  return result instanceof Object ? result : obj
}

```

