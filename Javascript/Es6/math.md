# 数学运算

1. 最大安全整数

   ```javascript
   Number.MAX_SAFE_INTEGER === 2**53-1
   Number.isSafeInteger(2**53-1)
   ```

   

2. 幂运算

   ```javascript
   Math.pow(x,y)
   x**y
   x**(1/y)
   ```

   

3. 取整运算

   ```javascript
   parseInt(x,10)
   Math.trunc(x) 
   // 按位非运算
   ~~x
   // 按位或运算
   x|0
   ```

4. 根运算

   ```javascript
   // 平方和的平方根
   Math.hypot([x[,y[,…]]]) 
   (x**2+y**2)**0.5
   x**(1/y)
   ```

5. 对数运算

   ```javascript
   Math.log(x)/Math.log(y)
   Math.log10(x) 
   // 返回以10为底数的x的对数。
   Math.log2(x) 
   // 返回以2为底数的x的对数。
   ```

   log<sub>x</sub><sup>z</sup>= ln<sup>z</sup>/ln<sup>x</sup>

