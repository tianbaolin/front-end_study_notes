1. then 方法返回值

```
1. 如果then中的回调函数返回一个值，那么then返回的Promise将会成为接受状态，并且将返回的值作为接受状态的回调函数的参数值。
2. 如果then中的回调函数抛出一个错误，那么then返回的Promise将会成为拒绝状态，并且将抛出的错误作为拒绝状态的回调函数的参数值。
3. 如果then中的回调函数返回一个已经是接受状态的Promise，那么then返回的Promise也会成为接受状态，并且将那个Promise的接受状态的回调函数的参数值作为该被返回的Promise的接受状态回调函数的参数值。
4. 如果then中的回调函数返回一个已经是拒绝状态的Promise，那么then返回的Promise也会成为拒绝状态，并且将那个Promise的拒绝状态的回调函数的参数值作为该被返回的Promise的拒绝状态回调函数的参数值。
5. 如果then中的回调函数返回一个未定状态（pending）的Promise，那么then返回Promise的状态也是未定的，并且它的终态与那个Promise的终态相同；同时，它变为终态时调用的回调函数参数与那个Promise变为终态时的回调函数的参数是相同的。
```

2. catch 与 [`Promise.prototype.then(undefined, onRejected)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then) 

   ```javascript
   1. 同一异常，onRejected 优先于catch处理,onRejected 处理后catch将捕获不到。两者作用域不一样
   let newPromise = (params) => {
     return new Promise((resolve, reject) => {
       setTimeout(() => {
         params ? resolve('正确') : reject('错误')
       }, 2000);
   
     }).then(res=>{
       console.log(res)
       return res
     },err=>{
       console.log(err)
       // return Promise.reject(err)
       return err
     }).catch(err=>{
       // 捕获不到错误
       console.log(err)
     }).then(res=>{
       // 始终进入
       console.log(res)
     })
   }
   2. 使用promise.then(onFulfilled, onRejected) 的话在 onFulfilled 中发生异常的话，在 onRejected 中是捕获不到这个异常的。在 promise.then(onFulfilled).catch(onRejected) 的情况下then 中产生的异常能在 .catch 中捕获
   
   function throwError(value) {
       // 抛出异常
       throw new Error(value);
   }
   // <1> onRejected不会被调用
   function badMain(onRejected) {
       return Promise.resolve(42).then(throwError, onRejected);
   }
   // <2> 有异常发生时onRejected会被调用
   function goodMain(onRejected) {
       return Promise.resolve(42).then(throwError).catch(onRejected);
   }
   // 运行示例
   badMain(function(){
       console.log("BAD");
   });
   goodMain(function(){
       console.log("GOOD");
   });
   3. .then 和 .catch 在本质上是没有区别的需要分场合使用。
   ```

3. promise

   - `Promise.prototype.catch`方法是`.then(null, rejection)`的别名，用于指定发生错误时的回调函数。建议总是使用`catch`方法，而不使用`then`方法的第二个参数。

   - 下面是异步加载图片的例子

     ```javascript
     function loadImageAsync(url) {
       return new Promise(function(resolve, reject) {
         const image = new Image();
     
         image.onload = function() {
           resolve(image);
         };
     
         image.onerror = function() {
           reject(new Error('Could not load image at ' + url));
         };
     
         image.src = url;
       });
     }
     
     const preloadImage = function (path) {
       return new Promise(function (resolve, reject) {
         const image = new Image();
         image.onload  = resolve;
         image.onerror = reject;
         image.src = path;
       });
     };
     ```

   - axios

     ```javascript
     axios.get('./data/a.json').then((message)=>{
       console.log(message)
       return axios.get('./data/c.json')
     }).then((message)=>{
       console.log(message)
     }).catch((error)=>{
       console.log(error.response)
     })
     ```

   - Async/await

     ```javascript
     function resolveAfter2Seconds() {
       return new Promise(resolve => {
         setTimeout(() => {
           resolve('resolved');
         }, 2000);
       });
     }
     
     async function asyncCall() {
       console.log('calling');
       // 等待promise 完成，但可以继续执行异步函数之外的code
       var result = await resolveAfter2Seconds();
       console.log(result);
       // expected output: "resolved"
     }
     
     asyncCall();
     
     ```



