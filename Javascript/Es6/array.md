# Array

1. 4字节字符长度判断

   ```javascript
   function length(str) {
     return [...str].length;
   }
   
   length('x\uD83D\uDE80y') // 3
   Array.from(string).length;
   ```

2. 任何定义了遍历器（Iterator）接口的对象（参阅 Iterator 一章），都可以用扩展运算符转为真正的数组。

   ```javascript
   Number.prototype[Symbol.iterator] = function*() {
     let i = 0;
     let num = this.valueOf();
     while (i < num) {
       yield i++;
     }
   }
   
   console.log([...5]) // [0, 1, 2, 3, 4]
   ```

3. Array.from()

   Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）

