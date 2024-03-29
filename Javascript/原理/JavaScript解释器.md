- 词法分析器（Lexical Analyser）
- 句法解析器（Syntax Parser）
- 字节码生成器（Bytecode generator）
- 字节码解释器（Bytecode interpreter）

## 词法分析器

词法分析器的作用，是将一行行的源码拆解成一个个词义单位（token）。所谓“词义单位”，指的是语法上不可能再分的、最小的单个字符或字符组合。

首先，词法分析器会扫描（scanning）代码，提取词义单位；然后，会进行评估（evaluating），判断词义单位属于哪一类的值。

词法分析是将字符流(char stream)转换为记号流(token stream)

```javascript
var sum = 30;

// 词法分析后的结果
[
  "var" : "keyword",
  "sum" : "identifier",
  "="   : "assignment",
  "30"  : "integer",
  ";"   : "eos" (end of statement)
]
```

上面代码中，源代码经过词法分析后，返回一组词义单位，以及它们各自的词类。

## 句法解析器

句法解析器的作用，是将上一步生成的数组，根据语法规则，转为抽象语法树（Abstract Syntax Tree，简称AST）。如果源码符合语法规则，这一步就会顺利完成，生成一个抽象语法树；如果源码存在语法错误，这一步就会终止，抛出一个“语法错误”。

```javascript
{
  operation: "=",
  left: {
    keyword: "var",
    right: "sum"
  }
  right: "30"
}
```

上面代码中，抽象语法树的一个节点是赋值操作符（=），它两侧的词义单位，分别成左侧子节点和右侧子节>点。

通常，这一步是整个JavaScript代码执行过程中最慢的。



## 预编译

js代码块通过语法分析阶段后，语法正确则进入预编译阶段。在分析预编译阶段之前，我们先了解一下js的**运行环境**，运行环境主要有三种：

- **全局环境**（JS代码加载完毕后，进入代码预编译即进入全局环境）
- **函数环境**（函数调用执行时，进入该函数环境，不同的函数则函数环境不同）
- **eval**（不建议使用，会有安全，性能等问题）

每进入一个不同的运行环境都会创建一个相应的**执行上下文（Execution Context）**

通过语法分析阶段后，进入预编译阶段，则创建执行上下文：

1. **创建变量对象（Variable Object）**

   1. **局部预编译的4个步骤：**
      1. 创建AO对象（Activation Object）函数执行上下文。
      2. 找**形参和变量声明**，将变量和形参名作为AO属性名，如果当前上下文的变量对象没有该变量名属性，则在该变量对象以变量名建立一个属性，属性值为**undefined**；如果存在，则忽略该变量声明
      3. 将实参值和形参统一。
      4. 创建**arguments对象**，检查当前上下文中的参数，建立该对象的属性与属性值，仅在函数环境(非箭头函数)中进行，全局环境没有此过程
      5. 查找**函数声明**，作为GO属性，值赋予函数体，属性值则为指向该函数所在堆内存地址的引用，如果存在，则会被新的引用覆盖。
   2.  **全局预编译的3个步骤：**
      1. 创建GO对象（Global Object）全局执行上下文。
      2. 查找**变量声明**，将变量名作为GO属性名，如果当前上下文的变量对象没有该变量名属性，则在该变量对象以变量名建立一个属性，属性值为**undefined**；如果存在，则忽略该变量声明
      3. 查找**函数声明**，作为GO属性，值赋予函数体，属性值则为指向该函数所在堆内存地址的引用，如果存在，则会被新的引用覆盖。

2. **建立作用域链（Scope Chain）**

   **作用域链由当前执行环境的变量对象（未进入执行阶段前）与上层环境的一系列活动对象组成，它保证了当前执行环境对符合访问权限的变量和函数的有序访问。**

3. **确定this的指向**



## 执行阶段

####js 运行时

<img src="./js_runtime.svg" alt="runtime" title="javascript runtime"/>

### 调用栈(call stack)

函数调用会在预编译阶段创建执行上下文，从栈顶压入形成了一个栈帧。

原始数据类型会存储在栈中

### 堆

对象被分配在一个堆中，即用以表示一大块非结构化的内存区域。

### 队列

一个 JavaScript 运行时包含了一个待处理的消息队列。每一个消息都关联着一个用以处理这个消息的函数。

在事件循环期间的某个时刻，运行时从最先进入队列的消息开始处理队列中的消息。为此，这个消息会被移出队列，并作为输入参数调用与之关联的函数。正如前面所提到的，调用一个函数总是会为其创造一个新的栈帧。

函数的处理会一直进行到执行栈再次为空为止；然后事件循环将会处理队列中的下一个消息（如果还有的话）。



####浏览器多线程

<img src="./brower_thred.jpg" width="200px"/>

<img src="./event_loop.jpg" width="300px"/>

GUI渲染线程

- 负责渲染浏览器界面，解析HTML，CSS，构建DOM树和RenderObject树，布局和绘制等。
- 当界面需要重绘（Repaint）或由于某种操作引发回流(reflow)时，该线程就会执行
- 注意，**GUI渲染线程与JS引擎线程是互斥的**，当JS引擎执行时GUI线程会被挂起（相当于被冻结了），GUI更新会被保存在一个队列中**等到JS引擎空闲时**立即被执行。

JS引擎线程

- 也称为JS内核，负责处理Javascript脚本程序。（例如V8引擎）
- JS引擎线程负责解析Javascript脚本，运行代码。
- JS引擎一直等待着任务队列中任务的到来，然后加以处理，一个Tab页（renderer进程）中无论什么时候都只有一个JS线程在运行JS程序
- 同样注意，**GUI渲染线程与JS引擎线程是互斥的**，所以如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞。

事件触发线程

- 归属于浏览器而不是JS引擎，用来控制事件循环（可以理解，JS引擎自己都忙不过来，需要浏览器另开线程协助）
- 当JS引擎执行代码块如setTimeOut时（也可来自浏览器内核的其他线程,如鼠标点击、AJAX异步请求等），会将对应任务添加到事件线程中
- 当对应的事件符合触发条件被触发时，该线程会把事件添加到待处理队列的队尾，等待JS引擎的处理
- 注意，由于JS的单线程关系，所以这些待处理队列中的事件都得排队等待JS引擎处理（当JS引擎空闲时才会去执行）

定时触发器线程

- 传说中的`setInterval`与`setTimeout`所在线程
- 浏览器定时计数器并不是由JavaScript引擎计数的,（因为JavaScript引擎是单线程的, 如果处于阻塞线程状态就会影响记计时的准确）
- 因此通过单独线程来计时并触发定时（计时完毕后，添加到事件队列中，等待JS引擎空闲后执行）
- 注意，W3C在HTML标准中规定，规定要求setTimeout中低于4ms的时间间隔算为4ms。

异步http请求线程

- 在XMLHttpRequest在连接后是通过浏览器新开一个线程请求
- 将检测到状态变更时，如果设置有回调函数，异步线程就**产生状态变更事件**，将这个回调再放入事件队列中。再由JavaScript引擎执行。

####事件循环进阶：macrotask与microtask

<img src="./job&task.jpg" width="300px">

macrotask（又称之为宏任务），可以理解是每次执行栈执行的代码就是一个宏任务（包括每次从事件队列中获取一个事件回调并放到执行栈中执行）

- 每一个task会从头到尾将这个任务执行完毕，不会执行其它
- 浏览器为了能够使得JS内部task与DOM任务能够有序的执行，会在一个task执行结束后，在下一个 task 执行开始前，对页面进行重新渲染 （`task->渲染->task->...`）

microtask（又称为微任务），可以理解是在当前 task 执行结束后立即执行的任务

- 也就是说，在当前task任务后，下一个task之前，在渲染之前
- 所以它的响应速度相比setTimeout（setTimeout是task）会更快，因为无需等渲染
- 也就是说，在某一个macrotask执行完后，就会将在它执行期间产生的所有microtask都执行完毕（在渲染前）

异步的实现可分为两个机制，分别是macro-task和micro-task。

Macrotasks包括: script（整体代码）、setTimeout, setInterval, setImmediate, I/O, UI Rendering；

Microtasks包括: process.nextTick, Promise, Object.observe, MutationObserver。

## 字节码生成器

字节码生成器的作用，是将抽象语法树转为JavaScript引擎可以执行的二进制代码。目前，还没有统一的JavaScript字节码的格式标准，每种JavaScript引擎都有自己的字节码格式。最简单的做法，就是将语义单位翻成对应的二进制命令。

## 字节码解释器

字节码解释器的作用是读取并执行字节码。