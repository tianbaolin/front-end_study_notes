1. 六大false 值
   * false
   * ""/''
   * 0
   * null
   * undefined
   * NaN

2. 六大原始数据类型（值类型）
   * String
   * Number 
   * Boolean
   * Undefined 
   * Null 
   * Symbol 

3. 原生自带遍历器
   * Array
   * String
   * Set
   * Map
   * Arguments
   * Dom NodeList
   * Generator 对象

4. 遍历方法
   * for/while循环
   * forEach 数组
   * for in 对象
   * for of 遍历器

5. 浅复制数组
   * [...[1,2,3]]
   * Array.from([1,2,3])
   * arr.slice()
   * arr.concat()

6. 浅复制对象
   * {…a}
   * Object.assign({},a)
   * Object.creat(a.constructor.prototype,Object.getOwnPropertyDescriptors(a))

7. 数组和字符串相互转换
   * arr.join('')
   * str.split('')
   * Array.from(str)
   * arr.reduce((acc,item)=>acc+item)
   * [...'hello']

8. 对象原型链上可枚举属性
   * for ... in
   * in

9. 判断类型
   * typeof
   * instanceof
   * constrcutor
   * Obiect.prototype.toString.call()

10. 相等比较
  * ===
  * ==
  * Object.is(a,b)

11. 进制转换
    * 十进制转二进制字符串 Number.prototype.toString(2)
    * Number.parseInt(string,2)

12. 构造函数与直接调用
    * new Object <=> Object
    * new Array <=> Array

13. Arguments 转 array
    * Array.from(arguments)
    * […arguments]
    * Array.prototype.slice.call(arguments)
    * Object.values(arguments)

14. 数字进值

    * 10 ：123456
    * 2 ：0b11110
    * 8 : 0O17
    * 16 : 0xf

15. 编码分类

    1. Unicode 编码

    * ASCII   0x00~0x7f  \u0000~\u007f 128个字符 一个字节

    * ANSI  扩展的ASCII编码 0x80~0xFFFF 各种文字自定义ANSI 两个字节 (GB2312、GBK、GB18030、Big5、Shift_JIS )

    * Unicode 总计13万 中日韩统一表意文字87,888 一个字符的Unicode编码是确定的。最多4个字节

      但是在实际传输过程中，由于不同系统平台的设计不一定一致，以及出于节省空间的目的，对Unicode编码的实现方式有所不同。Unicode的实现方式称为Unicode转换格式（Unicode Transformation Format，简称为UTF）

    * UTF-8 ：一种针对[Unicode](https://zh.wikipedia.org/wiki/Unicode)的可变长度[字符编码](https://zh.wikipedia.org/wiki/%E5%AD%97%E5%85%83%E7%B7%A8%E7%A2%BC)，也是一种[前缀码](https://zh.wikipedia.org/wiki/%E5%89%8D%E7%BC%80%E7%A0%81)。它可以用来表示Unicode标准中的任何字符，且其编码中的第一个[字节](https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82)仍与[ASCII](https://zh.wikipedia.org/wiki/ASCII)兼容。 1~4个字节。大部分汉语3个字节

    * UTF-16： 即把Unicode字符集的抽象[码位](https://zh.wikipedia.org/wiki/%E7%A0%81%E4%BD%8D)映射为16位长的整数（即[码元](https://zh.wikipedia.org/wiki/%E7%A0%81%E5%85%83)）的序列，用于数据存储或传递。Unicode字符的码位，需要1个或者2个16位长的码元来表示，因此这是一个变长表示。2/4个字节。

      大部分汉语两个字节，一个码元。

      **存储汉字 UTF-16 空间小于UTF-8。UTF-8变长，每个字节都需要存储字符的字节长度信息。**

      在JavaScript中，所有的string类型（或者被称为DOMString都是使用UTF-16编码的。

    2. Html /xml 转义

       与unicode编码一致，使用&#前缀+十进制表示。&#9784

    3. css转义

       与unicode编码一致，使用\前缀+十六进制表示。\21E1

    4. encodeURI

       是对统一资源标识符（URI）的组成部分进行编码的方法。它使用一到四个转义序列来表示字符串中的每个字符的UTF-8编码（只有由两个Unicode代理区字符组成的字符才用四个转义字符编码）。
       
    5. Base64 

       [**Base64**](https://zh.wikipedia.org/wiki/Base64)是一种基于64个可打印字符来表示[二进制数据](https://zh.wikipedia.org/wiki/二进制)的表示方法

       3个字节可由4个可打印字符来表示

       1.标准base64只有64个字符（英文大小写、数字和+、/）以及用作后缀等号；
       2.base64是把3个字节变成4个可打印字符，所以base64编码后的字符串一定能被4整除（不算用作后缀的等号）；
       3.等号一定用作后缀，且数目一定是0个、1个或2个。这是因为如果原文长度不能被3整除，base64要在后面添加\0凑齐3n位。为了正确还原，添加了几个\0就加上几个等号。显然添加等号的数目只能是0、1或2；
       4.严格来说base64不能算是一种加密，只能说是编码转换。使用base64的初衷。是为了方便把含有不可见字符串的信息用可见字符串表示出来，以便复制粘贴；

16. 数组作为参数使用，调用了iterator接口

    - for...of
    - Array.from()
    - Map(), Set(), WeakMap(), WeakSet()
    - Promise.all()
    - Promise.race()

17. 迭代器对象遍历方法

    * next 方法
    * for …of
    * 转换为数组 展开运算符
    
18. 严格模式主要有以下限制。

    - 变量必须声明后再使用
    - 函数的参数不能有同名属性，否则报错
    - 不能使用`with`语句
    - 不能对只读属性赋值，否则报错
    - 不能使用前缀 0 表示八进制数，否则报错
    - 不能删除不可删除的属性，否则报错
    - 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
    - `eval`不会在它的外层作用域引入变量
    - `eval`和`arguments`不能被重新赋值
    - `arguments`不会自动反映函数参数的变化
    - 不能使用`arguments.callee`
    - 不能使用`arguments.caller`
    - 禁止`this`指向全局对象
    - 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
    - 增加了保留字（比如`protected`、`static`和`interface`）

