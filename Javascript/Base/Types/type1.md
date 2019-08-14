### 1. [基本类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/A_re-introduction_to_JavaScript)

1. String

   ```javascript
   '12'
   'ad'
   "ded"
   let a = 'abc'
   tpyeof a // string
   let b = new String('abc')
   typeof b // object
   b[1] // b
   b.valueOf()//'abc'
   let c = String(123) //'123'
   
   `hello ${who}`
   
   let longString = "This is a very long string which needs \
   to wrap across multiple lines because \
   otherwise my code is unreadable.";
   ```

   | Code                     | Output              |
   | ------------------------ | ------------------- |
   | `\0`                     | 空字符              |
   | `\'`                     | 单引号              |
   | `\"`                     | `双引号`            |
   | `\\`                     | 反斜杠              |
   | `\n`                     | 换行                |
   | `\r`                     | `回车`              |
   | `\v`                     | 垂直制表符          |
   | `\t`                     | 水平制表符          |
   | `\b`                     | 退格                |
   | `\f`                     | 换页                |
   | `\uXXXX`                 | unicode 码          |
   | `\u{X}` ... `\u{XXXXXX}` | unicode codepoint   |
   | `\xXX`                   | Latin-1 字符(x小写) |

   ```javascript
   'asd'.charAt()// 'a'
   'asd'.charAt(3) // ""
   'asd'[1] //'s'
   'a' < 'b'
   'aa' <'b'
   
   var s_prim = "foo";
   var s_obj = new String(s_prim);
   console.log(typeof s_prim); // Logs "string"
   console.log(typeof s_obj);  // Logs "object"
   
   s1 = "2 + 2";               // creates a string primitive
   s2 = new String("2 + 2");   // creates a String object
   console.log(eval(s1));      // returns the number 4
   console.log(eval(s2));      // returns the string "2 + 2"
   ```

   ```javascript
   //使用 String() 方法将其它对象转化为字符串可以被认为是一种更加安全的做法，虽然该方法底层使用的也是 //toString() 方法，但是针对 null/undefined/symbols，String() 方法会有特殊的处理：
   String(123) //"123"
   String(0) //"0"
   String() //""
   String(false) //"false"
   String(true) //"true"
   String(null) //"null"
   String(NaN) //"NaN"
   String(undefined) //"undefined"
   
   String.length // 1
   String.fromCharCode(65,66,67) //"ABC"
   // 高位编码
   String.fromCodePoint(9731, 9733, 9842, 0x2F804)
   
   String.raw`templateString`
   // 字符串或者数组插值 输出字符串
   String.raw({raw:'123'},'a','b','c') //"1a2b3"
   String.raw({raw:[12,23,34]},'a','b') //"12a23b34"
   String.raw({raw:[12,23,34]},'a','b','d','e') //"12a23b34"
   String.raw({raw:[12,23,34,45]},'a','b','d','e') //"12a23b34d45"
   String.raw({raw:[12,23,34,45]},'a','b') //"12a23b3445"
   ```

   ```javascript
   '123'.charAt(3) // ""
   '123'[3] //undefined
   //返回表示给定索引的字符的Unicode的值。
   'AB'.charCodeAt(0) // 65
   'AB'.charCodeAt(-1) // NaN
   'ABC'.codePointAt(0);    // 66
   'XYZ'.codePointAt(42); // undefined
   
   '123'.concat(456,789) //"123456789"
   String.prototype.concat(123,456,789) //"123456789"
   
   str.includes(searchString[, position])
   var str = 'To be, or not to be, that is the question.';
   console.log(str.includes('To be'));       // true
   'ddsads'.includes() //false
   'ddsads'.includes('') //true
   
   'abcd'.indexOf('d',4) // -1
   'abcd'.indexOf('') // 0
   'abcd'.indexOf('',3) // 3
   'abcd'.indexOf('',10) // 4 
   'ddsads'.indexOf('a',-1) //3
   
   "canal".lastIndexOf("a")   // returns 3
   "canal".lastIndexOf("a",2) // returns 1
   "canal".lastIndexOf("a",0) // returns -1
   "canal".lastIndexOf("x")   // returns -1
   
   var str = "To be, or not to be, that is the question.";
   alert(str.startsWith("To be"));         // true
   alert(str.startsWith("not to be"));     // false
   alert(str.startsWith("not to be", 10)); // true
   
   var str = "To be, or not to be, that is the question.";
   alert( str.endsWith("question.") );  // true
   alert( str.endsWith("to be") );      // false
   alert( str.endsWith("to be", 19) );  // true
   'ddsads'.endsWith('dd',2) //true
   
   var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
   var regexp = /[A-E]/gi;
   var matches_array = str.match(regexp);
   console.log(matches_array);
   // ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
   
   'abc'.padEnd(10);          // "abc       "
   'abc'.padEnd(10, "foo");   // "abcfoofoof"
   'abc'.padEnd(6, "123456"); // "abc123"
   'abc'.padEnd(1);           // "abc"
   
   'abc'.padStart(10);         // "       abc"
   'abc'.padStart(10, "foo");  // "foofoofabc"
   'abc'.padStart(6,"123465"); // "123abc"
   'abc'.padStart(8, "0");     // "00000abc"
   'abc'.padStart(1);          // "abc"
   
   "abc".repeat(-1)     // RangeError: repeat count must be positive and less than //inifinity
   "abc".repeat(0)      // ""
   "abc".repeat(1)      // "abc"
   "abc".repeat(2)      // "abcabc"
   "abc".repeat(3.5)    // "abcabcabc" 参数count将会被自动转换成整数.
   "abc".repeat(1/0)    // RangeError: repeat count must be positive and less than //inifinity
   ({toString : () => "abc", repeat : String.prototype.repeat}).repeat(2)   
   //"abcabc",repeat是一个通用方法,也就是它的调用者可以不是一个字符串对象.
   
   let a = "abcabc"
   a.replace('a','1') //"1bcabc"
   a.replace('a','1').replace('a','1')  //"1bc1bc"
   a.replace(/abc/,'hello') //"helloabc"
   a.replace(/abc/g,'hello') //"helloabc"
   a.replace(/[a-zA-Z]/g,'hello') //"hellohellohellohellohellohello"
   
   let a = "abcabc"
   a.search(/abc/) //0
   a.search(/bc/) //1
   
   var str1 = 'The morning is upon us.';
   var str2 = str1.slice(4, -2);
   console.log(str2); // OUTPUT: morning is upon u
   var str = 'The morning is upon us.';
   str.slice(-3);     // returns 'us.'
   str.slice(-3, -1); // returns 'us'
   str.slice(0, -1);  // returns 'The morning is upon us'
   
   ''.split() //[""]
   ''.split('') //[]
   '   '.split('') // [" ", " ", " "]
   '12345'.split('') // ["1", "2", "3", "4", "5"]
   '12345'.split() //["12345"]
   '12345'.split(3) // ["12", "45"]
   '312 42342 423423 '.split(' ') // ["312", "42342", "423423", ""]
   '  312 42342 423423 '.split(' ') // ["", "", "312", "42342", "423423", ""]
   ' 312 42342 423423 '.split(' ',5) // ["", "312", "42342", "423423", ""]
   ' 312 42342 423423 '.split(' ',3) //["", "312", "42342"]
   
   'abcdfvdsv'.substr(-11,100) //"abcdfvdsv"
   'abcdfvdsv'.substr(2,4) //"cdfv"
   
   str.substring(indexStart[, indexEnd])
   //如果 indexStart 等于 indexEnd，substring 返回一个空字符串。
   //如果省略 indexEnd，substring 提取字符一直到字符串末尾。
   //如果任一参数小于 0 或为 NaN，则被当作 0。
   //如果任一参数大于 stringName.length，则被当作 stringName.length。
   //如果 indexStart 大于 indexEnd，则 substring 的执行效果就像两个参数调换了一样。
   var anyString = "Mozilla";
   // 输出 "Moz"
   console.log(anyString.substring(0,3));
   console.log(anyString.substring(3,0));
   console.log(anyString.substring(3,-3));
   console.log(anyString.substring(3,NaN));
   console.log(anyString.substring(-2,3));
   console.log(anyString.substring(NaN,3));
   // 输出 "lla"
   console.log(anyString.substring(4,7));
   console.log(anyString.substring(7,4));
   // 输出 ""
   console.log(anyString.substring(4,4));
   // 输出 "Mozill"
   console.log(anyString.substring(0,6));
   // 输出 "Mozilla"
   console.log(anyString.substring(0,7));
   console.log(anyString.substring(0,10));
   
   //String 对象覆盖了Object 对象的 toString 方法；并没有继承 Object.toString()。对于 String 
   //对象，toString 方法返回该对象的字符串形式，和 String.prototype.valueOf() 方法返回值一样。
   var x = new String("Hello world");
   alert(x.toString())      // 输出 "Hello world"
   
   a = new String(' csdc ') // String {" csdc "}
   a.trim() //"csdc"
   str.trimStart();
   str.trimLeft();
   str.trimEnd();
   str.trimRight();
   
   
   x = new String("Hello world");
   alert(x.valueOf())          // Displays "Hello world"
   //String 对象的 valueOf 方法返回一个String对象的原始值。该值等同于String.prototype.toString()
   
   str.toUpperCase()
   str.toLowerCase()
   str.toLocaleUpperCase()
   str.toLocaleLowerCase()
   
   var string = 'A\uD835\uDC68B\uD835\uDC69C\uD835\uDC6A';
   for (var v of string) {
     console.log(v);
   }
   // "A"
   // "\uD835\uDC68"
   // "B"
   // "\uD835\uDC69"
   // "C"
   // "\uD835\uDC6A"
   
   
   'asd'.link('baidu.com')
   //"<a href="baidu.com">asd</a>"
   'abc'.anchor('title')
   //"<a name="title">abc</a>"
   ```

   

2. Number

   ```javascript
   typeof Number //function
   typeof NaN // number
   typeof Infinity // number
   typeof -Infinity // number
   Math 是一个内置对象， 它具有数学常数和函数的属性和方法。不是一个函数对象。
   ```

   [paresInt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

   ```javascript
   Number.parseInt === parseInt // true
   parseInt(string, radix); // 2<=radix<=36 (26个字母+10个数字)
   // radix参数为n 将会把第一个参数看作是一个数的n进制表示，而返回的值则是十进制的。
   parseInt("123", 10); // 123
   parseInt("010", 10); //10
   parseInt("11", 2); // 3
   parseInt("010"); //10
   parseInt("0x10"); // 16
   parseInt("0x10",2) //0
   parseInt("0x10",8) //0
   parseInt("0x10",10); //0
   parseInt("0x10",16); //16
   parseInt("10",1); //NaN
   parseInt("10",36); //36
   parseInt("10",37); //NaN
   parseInt(0B11) //3
   parseInt(0o11) //9
   parseInt(0x11) //17
   //如果 parseInt 遇到了不属于radix参数所指定的基数中的字符那么该字符和其后的字符都将被忽略。接着返
   //回已经解析的整数部分。parseInt 将截取整数部分。开头和结尾的空白符允许存在，会被忽略。
   parseInt("6.022e23", 10); // 返回 6
   parseInt(6.022e2, 10);    // 返回 602
   parseInt('62a', 8);  //50
   //如果第一个字符不能被转换成数字，parseInt返回NaN。
   parseInt('62a', 2);  //NaN
   parseInt('434', 0);  //434
   //单元运算符 + 也可以把数字字符串转换成数值：
   + "42";   // 42
   + "010";  // 10
   + "0x10"; // 16
   parseInt(Infinity) //NaN
   ```

   parseFloat

   ```javascript
   //给定值被解析成浮点数。如果给定值不能被转换成数值，则会返回 NaN。
   //如果参数字符串的第一个字符不能被解析成为数字,则parseFloat返回NaN.
   parseFloat === Number.parseFloat
   parseFloat(Infinity) // Infinity
   parseFloat('Infinity') //Infinity
   parseFloat(34) //34
   ```

   [NaN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN)

   ```javascript
   //NaN 是一个全局对象的属性
   //NaN 属性的初始值就是 NaN，和 Number.NaN 的值一样。
   NaN == NaN // false
   NaN === NaN // false
   NaN == true //false
   NaN == false //false
   isNaN('32') // false
   isNaN('0x1') // false
   isNaN('12a') // true
   isNaN(NaN) // true
   isNaN() // true
   Number.isNaN()  // false
   isNaN(Infinity) // false
   Number.isNaN(NaN) // true
   //Number.isNaN() 方法确定传递的值是否为 NaN和其类型是 Number。它是原始的全局isNaN()的更强大的版
   //本。
   Number.isNaN('adc')  //false
   //缺少Number.isNaN函数的情况下, 通过表达式(x != x) 来检测变量x是否是NaN会更加可靠。
   typeof NaN // number
   '3' + NaN //"3NaN"
   ```

   Infinity

   ```javascript
   //Infinity 是全局对象（global object）的一个属性，即它是一个全局变量。
   //Infinity 是只读的
   Infinity === Number.POSITIVE_INFINITY
   -Infinity === Number.NEGATIVE_INFINITY
   //isFinite 方法检测它参数的数值。如果参数是 NaN，正无穷大或者负无穷大，会返回false，其他返回 true。
   isFinite(testValue)
   isFinite(1/0); // false 
   isFinite(Infinity); // false 
   isFinite(NaN); // false 
   isFinite(-Infinity); // false 
   isFinite(0); // true 
   isFinite(2e64); // true 
   isFinite("0"); // true
   //纯数值类型的检测，则返回false
   Number.isFinite("0"); // false
   ```

   Number

   ```javascript
   // 双精度 64 位二进制格式的值（-(2^63 -1) 到 2^63 -1）
   Number() //0
   Number('') //0
   Number('0') //l0
   Number(false) //0
   Number(true) //1
   Number([]) //0
   Number({}) //NaN
   Number(NaN) //NaN
   Number(undefined) //NaN
   Number(null) //0
   Number('0xf') //15
   Number('0xfh') // NaN
   Number() //0
   Number("0x11")    // 17
   Number("0b11")    // 3
   Number("0o11")    // 9
   // 微分基本单位
   Number.EPSILON // 2^-52
   //这里安全存储的意思是指能够准确区分两个不相同的值
   //超出此范围的整数值可能会被破坏。在工作中使用String 类型代替，是一个可行的解决方案
   Number.MAX_SAFE_INTEGER // 2^53-1
   Number.MIN_SAFE_INTEGER // -(2^53-1)
   Number.MAX_VALUE // 1.7976931348623157e+308
   -Number.MAX_VALUE 
   Number.MIN_VALUE  // 5e-324
   -Number.MIN_VALUE
   Number.NaN === NaN //false
   Number.POSITIVE_INFINITY
   Number.NEGATIVE_INFINITY
   
   Number.isNaN(NaN)
   Number.isFinite(0) //true
   // 不会强制将一个非数值的参数转换成数值
   Number.isFinite('12') // false
   // 是否整数
   Number.isInteger('43243') // false
   //确定传递的值是否为安全整数 ( -(2^53 - 1) 至 2^53 - 1之间)。
   Number.isSafeInteger()
   Number.parseFloat()
   //和全局对象 parseFloat() 一样。
   //Number.parseInt()
   和全局对象 parseInt() 一样。
   ```

   ```
   5
   05 //5
   0005 //5
   0b11 //3
   0o11 //9
   0x11 //17
   ```

   ```
   let a = new Number(5)
   typeof a // object
   let b = 5
   typeof b // number
   
   let a = 1000
   numObj.toExponential(fractionDigits)
   // 0<= fractionDigits <=20 执行环境也可以支持更大或更小范围。
   a.toExponential(2) // "1.00e3"
   345.6.toExponential(2) //"3.46e+2"
   //对数值字面量使用 toExponential() 方法，且该数值没有小数点和指数时，应该在该数值与该方法之间隔开
   //一个空格，以避免点号被解释为一个小数点。也可以使用两个点号调用该方法
   345 .toExponential(3) //"3.450e+2"
   33435..toExponential(4) //"3.3435e+4"
   
   numObj.toFixed(digits) // 0<= digits<=20
   3.432.toFixed(2) //"3.43"
   parseFloat(3.432.toFixed(2)) //3.43
   let e = new Number(5)
   e.toFixed(5) //"5.00000"
   
   numObj.toString([radix])
   // 指定要用于数字到字符串的转换的基数(从2到36)。如果未指定 radix 参数，则默认值为 10。
   e.toString() // "5"
   e.toString(2) //"101"
   e.toString(16) //"5"
   e = 1000
   e.toString(16) //"3e8"
   
   var number = 123456.789;
   console.log(number.toLocaleString('zh-Hans-CN-u-nu-hanidec'));
   //一二三,四五六.七八九
   
   numObj.toPrecision(precision)
   var numObj = 5.123456;
   numObj.toPrecision(2) //"5.1"
   (1234.5).toPrecision(2) //"1.2e+3"
   
   numObj.valueOf()
   //表示指定 Number 对象的原始值的数字
   var numObj = new Number(10);
   console.log(typeof numObj); // object
   var num = numObj.valueOf();
   console.log(num);           // 10
   console.log(typeof num);    // number
   ```

   

3. Boolean

   基本用法

   ```javascript
   a = new Boolean() //Boolean {false}
   a = new Boolean('') //Boolean {false}
   a = new Boolean('0') //Boolean {true}
   a = new Boolean(0) //Boolean {false}
   a = new Boolean(' ') //Boolean {true}
   a = new Boolean('false') //Boolean {true}
   a = new Boolean([]) // Boolean {true}
   a = new Boolean(undefined) //Boolean {false}
   a = new Boolean(null) //Boolean {false}
   a = new Boolean(NaN) //Boolean {false}
   ```

   ```javascript
   // 不要在应该使用基本类型布尔值的地方使用 Boolean 对象。
   Boolean() //false
   Boolean('') //false
   Boolean(0) //false
   Boolean(' ') //true
   Boolean(false) //false
   Boolean(null) //false
   Boolean(undefined) //false
   Boolean(NaN) //false
   Boolean(new Boolean(false)) //true
   Boolean('0') //true
   ```

   ```javascript
   Boolean.length //1
   Number.length //1
   String.length //1
   Array.length //1
   Object.length //1
   ```

   ```
   //构造函数的原型对象为其实例提供继承属性和方法。
   a.toString() //"true"
   a.valueOf() //true
   ```

   

4. Null

   ```
   //值 null 特指对象的值未设置。它是 JavaScript 基本类型 之一。
   //值 null 是一个字面量，它不像undefined 是全局对象的一个属性。null 是表示缺少的标识，指示变量未指
   //向任何对象。
   typeof null // object
   Boolean(null) //false
   null == 0 //false
   null == undefined //true
   null == '' //false
   null == false //false
   null == true //false
   typeof undefined   // "undefined"
   null === undefined // false
   null  == undefined // true
   null === null // true
   null == null // true
   !null //true
   isNaN(1 + null) // false
   isNaN(1 + undefined) // true
   window.null //undefined
   Object.prototype.__proto__ //null
   Object.getPrototypeOf(Object.prototype) //null
   '3'+ null //"3null"
   0/null //NaN
   NaN/null //NaN
   ```

   

5. Undefined

   ```
   //全局属性undefined表示原始值undefined。它是一个JavaScript的 原始数据类型 。
   window.undefined //undefined
   undefined in window //true
   undefined == null //true
   typeof undefined //"undefined"
   let x //undefined
   void(3) //undefined
   undefined == false //false
   undefined == true //false
   'undefined' in window //true
   0/undefined //NaN
   undefined + '4' //"undefined4"
   ```

   ```javascript
    null与undefined 区别 null == undefined 
   1. 意料之中的无 null表示"没有对象"，即该处不应该有值。 意料之外的无 undefined表示"缺少值"，就是此处应该有一个值 
   2. null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN
   3. null场景
    (1) 作为对象原型链的终点。 Object.prototype.__proto__ === null
    (2) 作为函数的参数，表示该函数的参数不是对象。
   4. undefined 场景
   （1）变量被声明了，但没有赋值时，就等于undefined。
   （2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。
   （3）对象没有赋值的属性，该属性的值为undefined。
   （4）函数没有返回值时，默认返回undefined。
   5. null 显示调用 undefined 隐式转换	
   ```

6. Symbol

   ```javascript
   1. 每个从Symbol()返回的symbol值都是唯一的。一个symbol值能作为对象属性的标识符；这是该数据类型仅有的目的。
   2. symbol 是一种基本数据类型 （primitive data type）
   3. Symbol 是一个创建symbol数据类型的函数
   a = Symbol() //Symbol()
   a.toLocaleString() //"Symbol()"
   a.valueOf() //Symbol()
   a.toString() //"Symbol()"
   a.constructor //ƒ Symbol() { [native code] }
   a.__proto__
   Symbol {constructor: ƒ, toString: ƒ, valueOf: ƒ, Symbol(Symbol.toStringTag): "Symbol", …}
   a.constructor === Symbol //true
   a.__proto__ === Symbol.prototype
   
   var sym1 = Symbol();
   var sym2 = Symbol('foo');
   var sym3 = Symbol('foo');
   Symbol("foo") === Symbol("foo"); // false
   
   var sym = Symbol("foo");
   typeof sym;     // "symbol"
   var symObj = Object(sym);
   typeof symObj;  // "object"
   
   a = Symbol('hello') //Symbol(hello)
   a.constructor === Symbol //true
   typeof a //"symbol"
   
   //Symbol.for(key) 方法会根据给定的键 key，来从运行时的 symbol 注册表中找到对应的 symbol，如果找
   //到了，则返回它，否则，新建一个与该键关联的 symbol，并放入全局 symbol 注册表中。
   a = Symbol('a') //Symbol(a)
   Symbol.for('a') === a //false, Symbol()方法创建的symbol不会放入全局symbol注册表 
   Symbol.for('a') === Symbol.for('a') //true
   
   a = Symbol.for('hello') //Symbol(hello)
   Symbol.keyFor(a) //"hello"
   // 创建一个 symbol，但不放入 symbol 注册表中
   var localSym = Symbol(); 
   Symbol.keyFor(localSym); // undefined，所以是找不到 key 的
   
   // Symbol类型数据作为属性名不可遍历
   Symbol("foo") !== Symbol("foo")
   const foo = Symbol()
   const bar = Symbol()
   typeof foo === "symbol"
   typeof bar === "symbol"
   let obj = {}
   obj[foo] = "foo"
   obj[bar] = "bar"
   JSON.stringify(obj) // {}
   Object.keys(obj) // []
   Object.getOwnPropertyNames(obj) // []
   Object.getOwnPropertySymbols(obj) // [ foo, bar ]
   
   const obj = {};
   let foo = Symbol("foo");
   Object.defineProperty(obj, foo, {
     value: "foobar",
   });
   for (let i in obj) {
     console.log(i); // 无输出
   }
   Object.getOwnPropertyNames(obj)
   // []
   Object.getOwnPropertySymbols(obj)
   
   //需要注意的是，Symbol.for为 Symbol 值登记的名字，是全局环境的，可以在不同的 iframe 或 service worker 中取到同一个值。
   let obj = {
     [Symbol('my_key')]: 1,
     enum: 2,
     nonEnum: 3
   };
   Reflect.ownKeys(obj) //  ["enum", "nonEnum", Symbol(my_key)]
   ```

   ```javascript
   // 除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法
   // 内置的 Symbol 值，提供元编程
   Symbol.hasInstance
   
   class MyClass {
     static [Symbol.hasInstance](foo) {
       console.log('12345')
       return false
     }
   }
   let c = new MyClass()
   console.log(c instanceof MyClass) // false
   
   // Symbol.iterator
   class Obj{
     *[Symbol.iterator](params) {
       console.log(this)
       for(let item of [1,2,3,4]){
         yield item
       }
     }
   }
   let obj = new Obj()
   for(let item of obj){
     console.log(item) // 1,2,3,4
   }
   
   Symbol.prototype.__proto__ === Object.prototype
   ```

   

