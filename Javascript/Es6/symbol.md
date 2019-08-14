1. **Symbol.hasInstance**

2. Symbol.isConcatSpreadable

   * 数组的默认行为是可以展开，`Symbol.isConcatSpreadable`默认等于`undefined`。该属性等于`true`时，也有展开的效果。

     类似数组的对象正好相反，默认不展开。它的`Symbol.isConcatSpreadable`属性设为`true`，才可以展开。

3. Symbol.species

   * 创建衍生对象时就会使用这个属性返回的函数，作为构造函数

4. Symbol.match

5. Symbol.search

6. Symbol.replace

7. Symbol.split

8. **Symbol.iterator**

   * 对象的`Symbol.iterator`属性，指向该对象的默认遍历器方法。

9. **Symbol.toPrimitive**

10. Symbol.toStringTag 

11. Symbol.unscopables

