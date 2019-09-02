



### Object

#### base

```javascript
1. 初始化
a = {
  count:0,
  set name(item){
    this.count += 1;
    return item;
  },
  get name(){
    return this.count
  }
}
a.name = 1
a.name = 2
a.name = 3
console.log(a.name)

2. 计算属性名
let key = 'name';
a={
  [key]:key
}
console.log(a)
a = {
  'name':'name'
}
console.log(a['name'])

3. 简写
var a = 'foo', 
    b = 42, 
    c = {};
// Shorthand property names (ES2015)
var o = {a, b, c};

// In other words,
console.log((o.a === {a}.a)); // true

4. 扩展属性
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// Object { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }

5. 变更原型

//定义属性为__proto__: 值 或 "__proto__": 值 时，不会创建名为__proto__属性。如果给出的值是对象或者null，那么对象的[[Prototype]]会被设置为给出的值。（如果给出的值不是对象也不是null，那么对象的原型不会改变。）
//在对象字面值中，仅有一次变更原型的机会；多次变更原型，会被视为语法错误。
//不使用冒号标记的属性定义，不会变更对象的原型；而是和其他具有不同名字的属性一样是普通属性定义。
```

```
对象的成员分类
1. 按用途分类：属性和方法
2. 按标识符分类：字面量和变量(主要针对属性)
3. 按定义方式：访问者成员和值成员(主要针对属性)
```

## `Object`构造函数的方法

```javascript
Object.length
Object.prototype
// Object 原型对象为原型链顶端，该对象没有原型了
Object.prototype.__proto__ = null
Object.prototype.constructor === Object
Object.constructor === Function
Object.__proto__.__proto__ === Object.prototype
Function.prototype.__proto__ === Object.prototype
Function.__proto__.__proto__ == Object.prototype
Function.__proto__ === Function.prototype === Object.__proto__=== (function(){}).__proto__
Function.constructor === Function
({}).__proto__ === Object.prototype
(function(){}).prototype.__proto__ === Object.prototype
```

```javascript
Object 
//Object构造函数为给定值创建一个对象包装器。如果给定值是 null 或 undefined，将会创建并返回一个空对象，否则，将返回一个与给定值对应类型的对象。

//当以非构造函数形式被调用时，Object 等同于 new Object()。

//以下对象原型相等
a = {}
b = new Object()
c = new Object({})
d = Object(null)
e = Object(undefined)

// new 操作符 的含义
1.创建一个对象(没有自身属性和方法)，指明其原型对象
2.将原型对象的constructor方法指向构造函数，
3.将该对象绑定到this并传递给构造函数。
4.执行构造函数
5.如果构造函数返回值为对象，new 操作符返回该对象否则返回之前创建的对象
function creatObject(x,y){
  let obj = Object.create({
    '__proto__':Object.prototype,
    constructor:creatObject
  })
  this = obj
  this.x = x;
  this.y = y
  return this
}
let obj = creatObject(x,y)
```

```javascript
Object.assign(target, ...sources)
//如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。
//Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。
//针对深拷贝，需要使用其他办法，因为 Object.assign()拷贝的是属性值。假如源对象的属性值是一个对象的引用，那么它也只指向那个引用。
const o1 = { a: 1 };
const o2 = { [Symbol('foo')]: 2 };
const obj = Object.assign({}, o1, o2);
console.log(obj); // { a : 1, [Symbol("foo")]: 2 } (cf. bug 1207182 on Firefox)
Object.getOwnPropertySymbols(obj); // [Symbol(foo)]
//继承属性和不可枚举属性是不能拷贝的
const obj = Object.create({foo: 1}, { // foo 是个继承属性。
    bar: {
        value: 2  // bar 是个不可枚举属性。
    },
    baz: {
        value: 3,
        enumerable: true  // baz 是个自身可枚举属性。
    }
});
const copy = Object.assign({}, obj);
console.log(copy); // { baz: 3 }

//原始类型会被包装为对象
const v1 = "abc";
const v2 = true;
const v3 = 10;
const v4 = Symbol("foo")

const obj = Object.assign({}, v1, null, v2, undefined, v3, v4); 
// 原始类型会被包装，null 和 undefined 会被忽略。
// 注意，只有字符串的包装对象才可能有自身可枚举属性。
console.log(obj); // { "0": "a", "1": "b", "2": "c" }

//拷贝访问器
const obj = {
  foo: 1,
  get bar() {
    return 2;
  }
};
let copy = Object.assign({}, obj); 
console.log(copy); // { foo: 1, bar: 2 } copy.bar的值来自obj.bar的getter函数的返回值
```

```javascript
Object.create(proto, [propertiesObject])
a = {}
Object {  }
b = new Object()
Object {  }
c = Object.create(Object.prototype)
Object {  }
a.__proto__ === b.__proto__
true
b.__proto__ == c.__proto__
true
c.__proto__ ===Object.prototype
true

o = {};
// 以字面量方式创建的空对象就相当于:
o = Object.create(Object.prototype);

//用 Object.create实现类式继承
// Shape - 父类(superclass)
function Shape() {
  this.x = 0;
  this.y = 0;
}

// 父类的方法
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};

// Rectangle - 子类(subclass)
function Rectangle() {
  Shape.call(this); // call super constructor.
}

// 子类续承父类
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;

var rect = new Rectangle();

console.log('Is rect an instance of Rectangle?',
  rect instanceof Rectangle); // true
console.log('Is rect an instance of Shape?',
  rect instanceof Shape); // true
rect.move(1, 1); // Outputs, 'Shape moved.'

// 继承到多个对象，则可以使用混入的方式
function MyClass() {
     SuperClass.call(this);
     OtherSuperClass.call(this);
}

// 继承一个类
MyClass.prototype = Object.create(SuperClass.prototype);
// 混合其它
Object.assign(MyClass.prototype, OtherSuperClass.prototype);
// 重新指定constructor
MyClass.prototype.constructor = MyClass;

MyClass.prototype.myMethod = function() {
     // do a thing
};

function Constructor(){}
o = new Constructor();
// 上面的一句就相当于:
o = Object.create(Constructor.prototype);
// 当然,如果在Constructor函数中有一些初始化代码,Object.create不能执行那些代码
```

```javascript
Object.defineProperty(obj, prop, descriptor)
Object.defineProperties(obj, props)
//该方法允许精确添加或修改对象的属性。通过赋值操作添加的普通属性是可枚举的，能够在属性枚举期间呈现出来（for...in 或 Object.keys 方法）， 这些属性的值可以被改变，也可以被删除。这个方法允许修改默认的额外选项（或配置）。默认情况下，使用 Object.defineProperty() 添加的属性值是不可修改的

// 属性分为值属性和访问者属性
1. 继承属性
如果访问者的属性是被继承的，它的 get 和set 方法会在子对象的属性被访问或者修改时被调用。如果这些方法用一个变量存值，该值会被所有对象共享。

function myclass() {
}
var value;
Object.defineProperty(myclass.prototype, "x", {
  get() {
    return value;
  },
  set(x) {
    value = x;
  }
});

var a = new myclass();
var b = new myclass();
a.x = 1;
console.log(b.x); // 1
//这可以通过将值存储在另一个属性中解决。在 get 和 set 方法中，this 指向某个被访问和修改属性的对象。
function myclass() {
}

Object.defineProperty(myclass.prototype, "x", {
  get() {
    return this.stored_x;
  },
  set(x) {
    this.stored_x = x;
  }
});

var a = new myclass();
var b = new myclass();
a.x = 1;
console.log(b.x); // 

//不像访问者属性，值属性始终在对象自身上设置，而不是一个原型。然而，如果一个不可写的属性被继承，它仍然可以防止修改对象的属性。
function myclass() {
}

myclass.prototype.x = 1;
Object.defineProperty(myclass.prototype, "y", {
  writable: false,
  value: 1
});

var a = new myclass();
a.x = 2;
console.log(a.x); // 2
console.log(myclass.prototype.x); // 1
a.y = 2; // Ignored, throws in strict mode
console.log(a.y); // 1
console.log(myclass.prototype.y); // 1

```

```javascript
Object.entries(obj)
//Object.entries()返回一个数组，其元素是与直接在object上找到的可枚举属性键值对相对应的数组。属性的顺序与通过手动循环对象的属性值所给出的顺序相同。
const obj = { foo: 'bar', baz: 42 };
console.log(Object.entries(obj)); // [ ['foo', 'bar'], ['baz', 42] ]
// array like object
const obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.entries(obj)); // [ ['0', 'a'], ['1', 'b'], ['2', 'c'] ]
// array like object with random key ordering
const anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.entries(anObj)); // [ ['2', 'b'], ['7', 'c'], ['100', 'a'] ]
// getFoo is property which isn't enumerable
const myObj = Object.create({}, { getFoo: { value() { return this.foo; } } });
myObj.foo = 'bar';
console.log(Object.entries(myObj)); // [ ['foo', 'bar'] ]
// non-object argument will be coerced to an object
console.log(Object.entries('foo')); // [ ['0', 'f'], ['1', 'o'], ['2', 'o'] ]
// iterate through key-value gracefully
const obj = { a: 5, b: 7, c: 9 };
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
}
// Or, using array extras
Object.entries(obj).forEach(([key, value]) => {
console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
});
var obj = { foo: "bar", baz: 42 }; 
var map = new Map(Object.entries(obj));
console.log(map); // Map { foo: "bar", baz: 42 }

Object.keys(obj)
//Object.keys 返回一个所有元素为字符串的数组，其元素来自于从给定的object上面可直接枚举的属性。这些属性的顺序与手动遍历该对象属性时的一致。
// simple array
var arr = ['a', 'b', 'c'];
console.log(Object.keys(arr)); // console: ['0', '1', '2']

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); // console: ['0', '1', '2']

// array like object with random key ordering
var anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(anObj)); // console: ['2', '7', '100']

// getFoo is a property which isn't enumerable
var myObj = Object.create({}, {
  getFoo: {
    value: function () { return this.foo; }
  } 
});
myObj.foo = 1;
console.log(Object.keys(myObj)); // console: ['foo']
```

```javascript
Object.freeze(obj)
Object.isFrozen(obj)
//Object.freeze() 方法可以冻结一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改。freeze() 返回和传入的参数相同的对象。
//被冻结的对象是不可变的。但也不总是这样。下例展示了冻结对象不是常量对象（浅冻结）。
obj1 = {
  internal: {}
};
Object.freeze(obj1);
obj1.internal.a = 'aValue';
obj1.internal.a // 'aValue'

//Object.seal()方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。
Object.seal(obj)
Object.isSealed(obj)
//Object.isSealed() 方法判断一个对象是否被密封。

//Object.preventExtensions()方法让一个对象变的不可扩展，也就是永远不能再添加新的属性。
//Object.preventExtensions()仅阻止添加自身的属性。但属性仍然可以添加到对象原型。
Object.preventExtensions(obj)
//Object.isExtensible() 方法判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）。
Object.isExtensible(obj)

Object.is()
//Object.is() 判断两个值是否相同。如果下列任何一项成立，则两个值相同：
//两个值都是 undefined
//两个值都是 null
//两个值都是 true 或者都是 false
//两个值是由相同个数的字符按照相同的顺序组成的字符串
//两个值指向同一个对象
//两个值都是数字并且
//都是正零 +0
//都是负零 -0
//都是 NaN
//都是除零和 NaN 外的其它同一个数字
```

```
Object.entries()
//返回给定对象自身可枚举属性的[key, value]数组。
Object.keys()
返回一个包含所有给定对象自身可枚举属性名称的数组。
Object.values()
返回给定对象自身可枚举值的数组
```

```javascript
Object.getOwnPropertyDescriptor()
//返回对象指定的属性配置。
Object.getOwnPropertyNames()
//返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名。
Object.getOwnPropertySymbols()
//返回一个数组，它包含了指定对象自身所有的符号属性。
Object.defineProperty()
//给对象添加一个属性并指定该属性的配置。
Object.defineProperties()
//给对象添加多个属性并分别指定它们的配置。
Object.getPrototypeOf()
//返回指定对象的原型对象。
Object.setPrototypeOf()
//设置对象的原型（即内部[[Prototype]]属性）。
```

## `Object` 实例和`Object` 原型对象

```javascript
Object.prototype.constructor === Object
Object.constructor === Function
Function.constructor === Function
Function.prototype.__proto__ === Object.prototype
```

```javascript
Object.prototype.hasOwnProperty()
//返回一个布尔值 ，表示某个对象是否含有指定的属性，而且此属性非原型链继承的。
Object.prototype.isPrototypeOf()
//返回一个布尔值，表示指定的对象是否在本对象的原型链中。
Object.prototype.propertyIsEnumerable()
//判断指定属性是否可枚举，内部属性设置参见 ECMAScript [[Enumerable]] attribute 。
Object.prototype.toLocaleString()
//直接调用 toString()方法。
Object.prototype.toString()
//返回对象的字符串表示。
Object.prototype.valueOf()
```



#### type

1. Array

   ```javascript
   Array.length === 1
   //只能用整数作为数组元素的索引，而不能用字符串。
   new Array(1,2,3,4) 与 Array(1,2,3,4) 等价
   //Array.from() 方法从一个类似数组或可迭代对象中创建一个新的数组实例。
   类型数组
   关联数组
   ```

   ```
   Array.from('foo'); 
   // ["f", "o", "o"]
   let s = new Set(['foo', window]); 
   Array.from(s); 
   // ["foo", window]
   let m = new Map([[1, 2], [2, 4], [4, 8]]);
   Array.from(m); 
   // [[1, 2], [2, 4], [4, 8]]
   function f() {
     return Array.from(arguments);
   }
   f(1, 2, 3);
   Array.from([1, 2, 3], x => x + x);  
   // x => x + x代表这是一个函数，只是省略了其他的定义，这是一种Lambda表达式的写法
   // 箭头的意思表示从当前数组中取出一个值，然后自加，并将返回的结果添加到新数组中    
   // [2, 4, 6]
   Array.from({length: 5}, (v, i) => i);
   // [0, 1, 2, 3, 4]
   ```

   ```
   //Array.isArray(obj)
   //当检测Array实例时, Array.isArray 优于 instanceof
   // 鲜为人知的事实：其实 Array.prototype 也是一个数组。
   Array.isArray(Array.prototype)
   true
   Array.prototype instanceof Array
   false
   ```

   ```javascript
   // Array.of() 和 Array 构造函数之间的区别在于处理整数参数：Array.of(7) 创建一个具有单个元素 7 的数组，而 Array(7) 创建一个长度为7的空数组（注意：这是指一个有7个空位的数组，而不是由7个undefined组成的数组）。
   Array.of(7);       // [7] 
   Array.of(1, 2, 3); // [1, 2, 3]
   Array(7);          // [ , , , , , , ]
   Array(1, 2, 3);    // [1, 2, 3]
   ```

   ```javascript
   Array.prototype.constructor === Array
   Array.prototype.length === 0
   ```

   ```javascript
   Array.prototype.pop()
   //删除数组的最后一个元素，并返回这个元素。
   Array.prototype.push()
   //在数组的末尾增加一个或多个元素，并返回数组的新长度。
   Array.prototype.unshift()
   //在数组的开头增加一个或多个元素，并返回数组的新长度。
   Array.prototype.shift()
   //删除数组的第一个元素，并返回这个元素。
   ```

   ```javascript
   Array.prototype.splice()
   //在任意的位置给数组添加或删除任意个元素。
   var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
   var removed = myFish.splice(2, 1, "trumpet");
   // 运算后的 myFish: ["angel", "clown", "trumpet", "surgeon"]
   // 被删除的元素: ["drum"]
   ```

   ```javascript
   
   Array.prototype.sort()
   //对数组元素进行排序，并返回当前数组。
   //要比较数字而非字符串，比较函数可以简单的以 a 减 b，如下的函数将会将数组升序排列
   function compareNumbers(a, b) {
     return a - b;
   }
   Array.prototype.reverse()
   //颠倒数组中元素的排列顺序，即原先的第一个变为最后一个，原先的最后一个变为第一个。
   ```

   ```javascript
   Array.prototype.indexOf()
   //返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。
   Array.prototype.lastIndexOf()
   //返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。
   Array.prototype.includes() 
   //判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false。
   [1, 2, 3].includes(3, 3);  // false
   [1, 2, 3].includes(3, -1); // true
   ```

   ```javascript
   Array.prototype.concat()
   //返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组。
   Array.prototype.join() //数组转字符串
   [1,2,3].join('') // '123'
   //连接所有数组元素组成一个字符串。
   Array.prototype.slice(arr) //浅复制一个数组
   //抽取当前数组中的一段元素组合成一个新数组。
   function list() {
     return Array.prototype.slice.call(arguments);
       // Array.from(arguments)
   }
   var list1 = list(1, 2, 3); // [1, 2, 3]
   var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
   var citrus = fruits.slice(1, 3);
   
   // fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
   // citrus contains ['Orange','Lemon']
   ```

   ```javascript
   Array.prototype.toString()
   //返回一个由所有数组元素组合而成的字符串。遮蔽了原型链上的 Object.prototype.toString() 方法。
   Array.prototype.toLocaleString()
   //返回一个由所有数组元素组合而成的本地化后的字符串。遮蔽了原型链上的 
   ```

   ```javascript
   Array.prototype.forEach()
   //为数组中的每个元素执行一次回调函数。
   ```

   ```javascript
   Array.prototype.entries() 
   //返回一个数组迭代器对象，该迭代器会包含所有数组元素的键值对。
   Array.prototype.keys() 
   //返回一个数组迭代器对象，该迭代器会包含所有数组元素的键。
   Array.prototype.values() 
   //返回一个数组迭代器对象，该迭代器会包含所有数组元素的值。
   ```

   ```javascript
   Array.prototype.every()
   //如果数组中的每个元素都满足测试函数，则返回 true，否则返回 false。
   Array.prototype.some()
   //如果数组中至少有一个元素满足测试函数，则返回 true，否则返回 false。
   Array.prototype.filter()
   //将所有在过滤函数中返回 true 的数组元素放进一个新数组中并返回。
   Array.prototype.map()
   //返回一个由回调函数的返回值组成的新数组。
   Array.prototype.reduce()
   // 累加 累乘
   //从左到右为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值。
   Array.prototype.reduceRight()
   //从右到左为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值。
   Array.prototype.find() 
   //找到第一个满足测试函数的元素并返回那个元素的值，如果找不到，则返回 undefined。
   Array.prototype.findIndex() 
   //找到第一个满足测试函数的元素并返回那个元素的索引，如果找不到，则返回 -1。
   ```

   

2. Function

   ```javascript
   //使用Function构造器生成的Function对象是在函数创建时解析的。这比你使用函数声明或者函数表达式(function)并在你的代码中调用更为低效，因为使用后者创建的函数是跟其他代码一起解析的。
   //以调用函数的方式调用Function的构造函数 (不是用new关键字) 跟以构造函数来调用是一样的.
   Function.prototype.constructor === Function
   true
   Function.constructor ===Function
   true
   Object.constructor === Function
   true
   typeof Function.prototype 
   "function"
   Function.prototype instanceof Function
   ```

   ```javascript
   new Function ([arg1[, arg2[, ...argN]],] functionBody)
   Function.length === 1
   Function.prototype.apply()
   //在一个对象的上下文中应用另一个对象的方法；参数能够以数组形式传入。
   Function.prototype.bind()
   //bind()方法会创建一个新函数,称为绑定函数.当调用这个绑定函数时,绑定函数会以创建它时传入 bind()方法的第一个参数作为 this,传入 bind()方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数.
   Function.prototype.call()
   //在一个对象的上下文中应用另一个对象的方法；参数能够以列表形式传入。
   Function.prototype.toString()
   //获取函数的实现源码的字符串。覆盖了 Object.prototype.toString 方法。
   ```

   

3. Map

   ```javascript
   //一个Object的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值，包括函数、对象、基本类型。
   //Map 中的键值是有序的，而添加到对象中的键则不是。因此，当对它进行遍历时，Map 对象是按插入的顺序返回键值。
   //你可以通过 size 属性直接获取一个 Map 的键值对个数，而 Object 的键值对个数只能手动计算。
   //Map 可直接进行迭代，而 Object 的迭代需要先获取它的键数组，然后再进行迭代。
   //Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。虽然 ES5 开始可以用 map = Object.create(null) 来创建一个没有原型的对象，但是这种用法不太常见。
   //Map 在涉及频繁增删键值对的场景下会有些性能优势。
   new Map([iterable])
   Map.prototype.size
   Map.length = 0
   new Map([['name','tbl'],['age':18]])
   ```

   ```javascript
   Map.prototype.clear()
   //移除Map对象的所有键/值对 。
   Map.prototype.delete(key)
   //如果 Map 对象中存在该元素，则移除它并返回 true；否则如果该元素不存在则返回 false
   Map.prototype.get(key)
   //返回键对应的值，如果不存在，则返回undefined。
   Map.prototype.has(key)
   //返回一个布尔值，表示Map实例是否包含键对应的值。
   Map.prototype.set(key, value)
   //设置Map对象中键的值。返回该Map对象。
   ```

   ```javascript
   Map.prototype.entries()
   //返回一个新的 Iterator 对象，它按插入顺序包含了Map对象中每个元素的 [key, value] 数组。
   Map.prototype.keys()
   //返回一个新的 Iterator对象， 它按插入顺序包含了Map对象中每个元素的键 。
   Map.prototype.values()
   //返回一个新的Iterator对象，它按插入顺序包含了Map对象中每个元素的值 。
   Map.prototype.forEach(callbackFn[, thisArg])
   //按插入顺序，为 Map对象里的每一键值对调用一次callbackFn函数。如果为forEach提供了thisArg，它将在每次回调中作为this值。
   Map.prototype[Symbol.iterator] === Map.prototype.entries
   ```

   ```javascript
   //Map对象间可以进行合并，但是会保持键的唯一性。
   var first = new Map([
     [1, 'one'],
     [2, 'two'],
     [3, 'three'],
   ]);
   
   var second = new Map([
     [1, 'uno'],
     [2, 'dos']
   ]);
   
   // 合并两个Map对象时，如果有重复的键值，则后面的会覆盖前面的。
   // 展开运算符本质上是将Map对象转换成数组。
   var merged = new Map([...first, ...second]);
   console.log(merged.get(1)); // uno
   console.log(merged.get(2)); // dos
   console.log(merged.get(3)); // three
   // 浅复制
   var original = new Map([
     [1, 'one']
   ]);
   var clone = new Map(original);
   ```

   

4. Set(集合)

   ```javascript
   // Set对象是值的集合，你可以按照插入的顺序迭代它的元素。 Set中的元素只会出现一次，即 Set 中的元素是唯一的。
   Set.length === 0
   Set.prototype.size
   //返回Set对象的值的个数。
   new Set([1,2,3,4])
   ```

   ```javascript
   Set.prototype.add(value)
   //在Set对象尾部添加一个元素。返回该Set对象。
   Set.prototype.clear()
   //移除Set对象内的所有元素。
   Set.prototype.delete(value)
   //移除Set的中与这个值相等的元素，返回Set.prototype.has(value)在这个操作前会返回的值（即如果该元素存在，返回true，否则返回false）。Set.prototype.has(value)在此后会返回false。
   Set.prototype.has(value)
   //返回一个布尔值，表示该值在Set中存在与否。
   
   ```

   ```javascript
   Set.prototype.entries()
   //返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值的[value, value]数组。为了使这个方法和Map对象保持相似， 每个值的键和值相等。
   Set.prototype.keys()
   //与values()方法相同，返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。
   Set.prototype.values()
   //返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。
   Set.prototype[Symbol.iterator] === Set.prototype.values
   
   Set.prototype.forEach(callbackFn[, thisArg])
   //按照插入顺序，为Set对象中的每一个值调用一次callBackFn。如果提供了thisArg参数，回调中的this会是这个参数。
   ```

   ```javascript
   function union(setA, setB) {
       var _union = new Set(setA);
       for (var elem of setB) {
           _union.add(elem);
       }
       return _union;
   }
   
   function intersection(setA, setB) {
       var _intersection = new Set();
       for (var elem of setB) {
           if (setA.has(elem)) {
               _intersection.add(elem);
           }
       }
       return _intersection;
   }
   
   function difference(setA, setB) {
       var _difference = new Set(setA);
       for (var elem of setB) {
           _difference.delete(elem);
       }
       return _difference;
   }
   ```

   ```javascript
   var myArray = ["value1", "value2", "value3"];
   
   // 用Set构造器将Array转换为Set
   var mySet = new Set(myArray);
   var text = 'Indiana';
   var mySet = new Set(text);  // Set {'I', 'n', 'd', 'i', 'a'}
   const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]
   console.log([...new Set(numbers)]) 
   // [2, 3, 4, 5, 6, 7, 32]
   ```

   

5. Date

   ```javascript
   //创建 Date 实例用来处理日期和时间。Date 对象基于1970年1月1日（世界标准时间）起的毫秒数。
   Date()
   "Thu Mar 21 2019 16:59:15 GMT+0800 (中国标准时间)"
   a = new Date()
   Thu Mar 21 2019 16:59:41 GMT+0800 (中国标准时间)
   new Date
   Thu Mar 21 2019 16:59:41 GMT+0800 (中国标准时间)
   new Date(Date())
   Thu Mar 21 2019 17:01:26 GMT+0800 (中国标准时间)
   ```

   ```javascript
   new Date(dateString);
   new Date(year, month[, day[, hour[, minutes[, seconds[, milliseconds]]]]]);
   Date.length === 7
   ```

   ```javascript
   Date.now()
   //返回自 1970-1-1 00:00:00  UTC (世界标准时间)至今所经过的毫秒数。
   Date.parse()
   //解析一个表示日期的字符串，并返回从 1970-1-1 00:00:00 所经过的毫秒数。
   Date.UTC()
   //接受和构造函数最长形式的参数相同的参数（从2到7），并返回从 1970-01-01 00:00:00 UTC 开始所经过的毫秒数。
   ```

   ```javascript
   
   //根据本地时间返回指定日期对象的月份中的第几天（1-31）。
   Date.prototype.getDay()
   //根据本地时间返回指定日期对象的星期中的第几天（0-6）。
   Date.prototype.getFullYear()
   //根据本地时间返回指定日期对象的年份（四位数年份时返回四位数字）。
   Date.prototype.getHours()
   //根据本地时间返回指定日期对象的小时（0-23）。
   Date.prototype.getMilliseconds()
   //根据本地时间返回指定日期对象的毫秒（0-999）。
   Date.prototype.getMinutes()
   //根据本地时间返回指定日期对象的分钟（0-59）。
   Date.prototype.getMonth()
   //根据本地时间返回指定日期对象的月份（0-11）。
   Date.prototype.getSeconds()
   //根据本地时间返回指定日期对象的秒数（0-59）。
   Date.prototype.getTime()
   //返回从1970-1-1 00:00:00 UTC（协调世界时）到该日期经过的毫秒数，对于1970-1-1 00:00:00 UTC之前的时间返回负值。
   ```

   ```javascript
   Date.prototype.setDate()
   //根据本地时间为指定的日期对象设置月份中的第几天。
   Date.prototype.setFullYear()
   //根据本地时间为指定日期对象设置完整年份（四位数年份是四个数字）。
   Date.prototype.setHours()
   //根据本地时间为指定日期对象设置小时数。
   Date.prototype.setMilliseconds()
   //根据本地时间为指定日期对象设置毫秒数。
   Date.prototype.setMinutes()
   //根据本地时间为指定日期对象设置分钟数。
   Date.prototype.setMonth()
   //根据本地时间为指定日期对象设置月份。
   Date.prototype.setSeconds()
   //根据本地时间为指定日期对象设置秒数。
   Date.prototype.setTime()
   //通过指定从 1970-1-1 00:00:00 UTC 开始经过的毫秒数来设置日期对象的时间，对于早于 1970-1-1 00:00:00 UTC的时间可使用负值。
   ```

   

6. RegExp

   ```javascript
   //RegExp 构造函数创建了一个正则表达式对象，用于将文本与一个模式匹配。
   //字面量, 构造函数和工厂符号都是可以的：
   /pattern/flags
   new RegExp(pattern [, flags])
   RegExp(pattern [, flags])
   /ab+c/i;
   new RegExp('ab+c', 'i');
   new RegExp(/ab+c/, 'i');
   RegExp.length === 2
   ```

   ```javascript
   RegExp.prototype.global
   //是否开启全局匹配，也就是匹配目标字符串中所有可能的匹配项，而不是只进行第一次匹配。
   RegExp.prototype.ignoreCase
   //在匹配字符串时是否要忽略字符的大小写。
   RegExp.prototype.lastIndex
   //下次匹配开始的字符串索引位置。
   RegExp.prototype.multiline
   //是否开启多行模式匹配（影响 ^ 和 $ 的行为）。
   ```

   ````javascript
   RegExp.prototype.exec()
   //在目标字符串中执行一次正则匹配操作。
   RegExp.prototype.test()
   //测试当前正则是否能匹配目标字符串。
   ````

   ```
   . // 任意单个字符
   [0-9] \d // 任意单个阿拉伯数字
   [^0-9] \D //任意单个不是阿拉伯数字
   [A-Za-z0-9_] \w // 匹配任意来自基本拉丁字母表中的字母数字字符，还包括下划线
   [^A-Za-z0-9_] \W// 匹配任意不是基本拉丁字母表中单词（字母数字下划线）字符的字符
   \s //空格
   \S //非空格
   [xyz] // 匹配集合中的任意一个字符。你可以使用连字符'-'指定一个范围。
   [^xyz]	// 它匹配任意不在括号内的字符。你也可以通过使用连字符 '-' 指定一个范围内的字符。
   ^ //开始
   $ // 结束
   (x) //匹配 x 并且捕获匹配项。 这被称为捕获括号（capturing parentheses）。
   x* // 匹配前面的模式 x 0 或多次
   x+ // 匹配前面的模式 x 1 或多次。等价于 {1,}。
   x? // 匹配前面的模式 x 0 或 1 次。
   x|y // 匹配 x 或 y
   x{n} // n 是一个正整数。前面的模式 x 连续出现 n 次时匹配。
   x{n,} // n 是一个正整数。前面的模式 x 连续出现至少 n 次时匹配。
   x{n,m} // n 和 m 为正整数。前面的模式 x 连续出现至少 n 次，至多 m 次时匹配。
   ```

   

7. Error

   ```javascript
   // this:
   const x = Error('I was created using a function call!');
   // has the same functionality as this:
   const y = new Error('I was constructed via the "new" keyword!');
   
   EvalError
   //创建一个error实例，表示错误的原因：与 eval() 有关。
   InternalError 
   //创建一个代表Javascript引擎内部错误的异常抛出的实例。 如: "递归太多".
   RangeError
   //创建一个error实例，表示错误的原因：数值变量或参数超出其有效范围。
   ReferenceError
   //创建一个error实例，表示错误的原因：无效引用。
   SyntaxError
   //创建一个error实例，表示错误的原因：eval()在解析代码的过程中发生的语法错误。
   TypeError
   //创建一个error实例，表示错误的原因：变量或参数不属于有效类型。
   URIError
   创建一个error实例，表示错误的原因：给 encodeURI()或  decodeURl()传递的参数无效。
   ```

8. ArrayBuffer/TypedArray/TypedArray

   1. `ArrayBuffer`对象、`TypedArray`视图和`DataView`视图是 JavaScript 操作二进制数据的一个接口。

   **（1）ArrayBuffer对象**：代表内存之中的一段二进制数据，可以通过“视图”进行操作。“视图”部署了数组接口，这意味着，可以用数组的方法操作内存。

   **（2）TypedArray视图**：共包括 9 种类型的视图，比如`Uint8Array`（无符号 8 位整数）数组视图, `Int16Array`（16 位整数）数组视图, `Float32Array`（32 位浮点数）数组视图等等。

   **（3）DataView视图**：可以自定义复合格式的视图，比如第一个字节是 Uint8（无符号 8 位整数）、第二、三个字节是 Int16（16 位整数）、第四个字节开始是 Float32（32 位浮点数）等等，此外还可以自定义字节序。

   简单说，`ArrayBuffer`对象代表原始的二进制数据，`TypedArray`视图用来读写简单类型的二进制数据，`DataView`视图用来读写复杂类型的二进制数据。

   2. 应用
      1. Ajax
      2. Fetch API
      3. Web socket
      4. Web worker
      5. File API
      6. Canvas
   3. SharedArrayBuffer
   4. Atomics
      1. **Atomics.store()，Atomics.load()**
      2. **Atomics.exchange()**
      3. **Atomics.wait()，Atomics.wake()**
      4. **Atomics.add()**, **Atomics.sub()**

