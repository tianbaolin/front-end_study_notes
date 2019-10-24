## Class

### 1. 基本使用

```javascript
class People {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  say() {
    console.log('object :', 'people');
    console.log('this.y :', this.y);
  }
}
function People2(x, y) {
  this.x = x;
  this.y = y;
}
People2.prototype.say = function say() {
  console.log('object :', 'people2');
  console.log('this.y :', this.y);
};

class Man extends People {
  constructor(x, y, z) {
    super(x, y);
    this.z = z;
  }

  say() {
    console.log('this.z :', this.z);
    console.log('object :', 'man');
  }
}

function Man2(x, y, z) {
  People2.call(this, x, y);
  this.z = z;
}
Object.setPrototypeOf(Man2.prototype, People2.prototype);
Man2.prototype.say = function say() {
  console.log('this.z :', this.z);
  console.log('object :', 'man');
};
const man = new Man(3, 4, 5);
const man2 = new Man2(3, 4, 5);
console.assert(man.__proto__.__proto__ === People.prototype);
console.assert(man2.__proto__.__proto__ === People2.prototype);
console.log(man, man2);
```

### 2. Spuer

`super`这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

#### 1. 当作方法

`super`虽然代表了父类`A`的构造函数，但是返回的是子类`B`的实例，即`super`内部的`this`指的是`B`的实例，因此`super()`在这里相当于`A.prototype.constructor.call(this)`。作为函数时，`super()`只能用在子类的构造函数之中，用在其他地方就会报错。

```javascript
class A {
  constructor() {
    console.log(new.target.name);
  }
}
class B extends A {
  constructor() {
    super();
  }
}
new A() // A
new B() // B
```

####2. 当作对象

第二种情况，`super`作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。

```javascript
class A {
  p() {
    return 2;
  }
}

class B extends A {
  constructor() {
    super();
    console.log(super.p()); // 2
  }
}

let b = new B();
```

这里需要注意，由于`super`指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过`super`调用的。

```javascript
class A {
  constructor() {
    this.p = 2;
  }
}

class B extends A {
  get m() {
    return super.p;
  }
}

let b = new B();
b.m // undefined
```

上面代码中，`p`是父类`A`实例的属性，`super.p`就引用不到它。

如果属性定义在父类的原型对象上，`super`就可以取到。

ES6 规定，在子类普通方法中通过`super`调用父类的方法时，方法内部的`this`指向当前的子类实例。

```javascript
class A {
  constructor() {
    this.x = 1;
  }
  print() {
    console.log(this.x);
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
  }
  m() {
    super.print();
  }
}

let b = new B();
b.m() // 2
```

`super.print()`虽然调用的是`A.prototype.print()`，但是`A.prototype.print()`内部的`this`指向子类`B`的实例，导致输出的是`2`，而不是`1`。也就是说，实际上执行的是`super.print.call(this)`。由于`this`指向子类实例，所以如果通过`super`对某个属性赋值，这时`super`就是`this`，赋值的属性会变成子类实例的属性。

```javascript
class A {
  constructor() {
    this.x = 1;
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
    super.x = 3;
    console.log(super.x); // undefined
    console.log(this.x); // 3
  }
}

let b = new B();
```

如果`super`作为对象，用在静态方法之中，这时`super`将指向父类，而不是父类的原型对象。

```javascript
class Parent {
  static myMethod(msg) {
    console.log('static', msg);
  }

  myMethod(msg) {
    console.log('instance', msg);
  }
}

class Child extends Parent {
  static myMethod(msg) {
    super.myMethod(msg);
  }

  myMethod(msg) {
    super.myMethod(msg);
  }
}

Child.myMethod(1); // static 1

var child = new Child();
child.myMethod(2); // instance 2
```

另外，在子类的静态方法中通过`super`调用父类的方法时，方法内部的`this`指向当前的子类，而不是子类的实例。

```javascript
class A {
  constructor() {
    this.x = 1;
  }
  static print() {
    console.log(this.x);
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
  }
  static m() {
    super.print();
  }
}

B.x = 3;
B.m() // 3
```

注意，使用`super`的时候，必须显式指定是作为函数、还是作为对象使用，否则会报错。

```javascript
class A {}

class B extends A {
  constructor() {
    super();
    console.log(super); // 报错
  }
}
```

最后，由于对象总是继承其他对象的，所以可以在任意一个对象中，使用`super`关键字。

### 3. 类的 prototype 属性和__proto__属性

Class 作为构造函数的语法糖，同时有`prototype`属性和`__proto__`属性，因此同时存在两条继承链。

（1）子类的`__proto__`属性，表示构造函数的继承，总是指向父类。

（2）子类`prototype`属性的`__proto__`属性，表示方法的继承，总是指向父类的`prototype`属性。

```javascript
class People {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  say() {
    console.log('this :', this);
  }
}
console.log(People.prototype.__proto__ === Object.prototype);
console.log(People.__proto__ === Function.__proto__);
```

```javascript
class A {
}

class B extends A {
}

B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true
```

这两条继承链，可以这样理解：作为一个对象，子类（`B`）的原型（`__proto__`属性）是父类（`A`）；作为一个构造函数，子类（`B`）的原型对象（`prototype`属性）是父类的原型对象（`prototype`属性）的实例。

```javascript
class A extends Object {
}

A.__proto__ === Object // true
A.prototype.__proto__ === Object.prototype // true
// 这种情况下，A其实就是构造函数Object的复制，A的实例就是Object的实例。
class A {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true
// 这种情况下，A作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承Function.prototype。但是，A调用后返回一个空对象（即Object实例），所以A.prototype.__proto__指向构造函数（Object）的prototype属性。
```

子类实例的`__proto__`属性的`__proto__`属性，指向父类实例的`__proto__`属性。也就是说，子类的原型的原型，是父类的原型。

```javascript
var p1 = new Point(2, 3);
var p2 = new ColorPoint(2, 3, 'red');

p2.__proto__ === p1.__proto__ // false
p2.__proto__.__proto__ === p1.__proto__ // true
```

### ES5与ES6继承区别

* ### ES5的继承机制总结

  ES5的继承机制简单来说就是：实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）

* ### ES6的继承机制总结

  先创建父类实例this 通过class丶extends丶super关键字定义子类，并改变this指向,super本身是指向父类的构造函数但做函数调用后返回的是子类的实例，实际上做了父类.prototype.constructor.call(this)，做对象调用时指向父类.prototype,从而实现继承。