## VUE vs REACT

*  Jsx VS template  =>render function

*  数据劫持js API （Object.defineProperty, Proxy）VS 原生实现观察者模式（PureComponent/shouldComponentUpdate） =>响应式数据（观察者模式）
* 功能组合 HoC（高阶组件，偏向于js 操作，更可控） 和 mixins（混入，对象合并Object.assign）=>装饰器模式
* 子父通信 自定义事件 VS  回调函数 => 基于回调函数
* Redux 使用的是不可变数据，而Vuex的数据是可变的。Redux每次都是用新的state替换旧的state，而Vuex是直接修改。