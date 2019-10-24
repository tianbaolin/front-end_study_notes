## Generator

### 1. 定义

* 语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。
* 执行 Generator 函数会返回一个遍历器对象
* 形式上，Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态

Generator 函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。不同的是，调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，也就是上一章介绍的遍历器对象（Iterator Object）。

下一步，必须调用遍历器对象的`next`方法，使得指针移向下一个状态。也就是说，每次调用`next`方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个`yield`表达式（或`return`语句）为止。换言之，Generator 函数是分段执行的，`yield`表达式是暂停执行的标记，而`next`方法可以恢复执行。

### 2. 分析

*  由于 Generator 函数返回的遍历器对象，只有调用`next`方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。`yield`表达式就是暂停标志。

* 遇到`yield`表达式，就暂停执行后面的操作，并将紧跟在`yield`后面的那个表达式的值，作为返回的对象的`value`属性值。

* Generator 函数可以不用`yield`表达式，这时就变成了一个单纯的暂缓执行函数。

* `yield`表达式只能用在 Generator 函数里面，用在其他地方都会报错。

* `yield`表达式本身没有返回值，或者说总是返回`undefined`。`next`方法可以带一个参数，该参数就会被当作上一个`yield`表达式的返回值。通过`next`方法的参数，就有办法在 Generator 函数开始运行之后，继续向函数体内部注入值。也就是说，可以在 Generator 函数运行的不同阶段，从外部向内部注入不同的值，从而调整函数行为。（实现异步控制流）

  ```javascript
  function* gen(x){
    var y = yield x + 2;
    return y;
  }
  
  var g = gen(1);
  g.next() // { value: 3, done: false }
  g.next(2) // { value: 2, done: true }
  ```

  

### 3. 应用

```javascript
function* main() {
  var result = yield request("http://some.url");
  var resp = JSON.parse(result);
    console.log(resp.value);
}

function request(url) {
  makeAjaxCall(url, function(response){
    // 需要在回调中手动调用next方法传入结果，衍生出了async await
    it.next(response);
  });
}

var it = main();
it.next();
```

### 4. 总结

1. generator函数返回一个迭代器对象（即使不使用yield）
2. 返回的迭代器对象可以使用for...of 遍历和next方法遍历