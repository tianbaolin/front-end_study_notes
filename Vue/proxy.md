## Proxy

#####Proxy是`Object.defineProperty`的全方位加强版

* Proxy可以直接监听对象而非属性
* Proxy可以直接监听对象方法的访问，包括数组

Proxy有多达13种拦截方法,不限于apply、ownKeys、deleteProperty、has等等是`Object.defineProperty`不具备的。