

## VUEX

### 1. 基本使用方法

* 定义

  ```javascript
  // 基本定义
  import Vue from 'vue';
  import Vuex from 'vuex';
  import products from './modules/products';
  
  Vue.use(Vuex);
  
  export default new Vuex.Store({
    state: {
      userName: '',
      token: '',
    },
    // 同步
    mutations: {
      login(state, data) {
        state.userName = data;
      },
      setToken(state, data) {
        state.token = data;
      },
    },
    actions: {
      getToken({ commit }, data) {
        setTimeout(() => {
          commit('setToken', data);
        }, 1000);
      },
    },
    getters: {
      tokenReverse(state) {
        return state.token
          .split('')
          .reverse()
          .join('');
      },
    },
    modules: {
      products,
    },
  });
  ```

  ```javascript
  // ./modules/products 模块化
  import { SET_PRODUCTS_MOUNT } from '../mutations_types';
  
  export default {
    namespaced: true,
    state: {
      iphone: 0,
    },
    getters: {},
    mutations: {
      [SET_PRODUCTS_MOUNT]: (state, amount) => {
        state.iphone += amount;
      },
    },
    actions: {},
  };
  ```

  ```javascript
  // ../mutations_types  定义mutations 方法名称，方便使用
  export const SET_PRODUCTS_MOUNT = 'SET_PRODUCTS_MOUNT';
  export default { SET_PRODUCTS_MOUNT };
  ```

  

* 使用

  ```javascript
  import { mapState, mapMutations, mapActions, mapGetters } from "vuex";
  import { SET_PRODUCTS_MOUNT } from "../store/mutations_types";
  // 利用map系列api简化书写，map返回一个对象
   computed: {
      ...mapState({
        userName: "userName",
        token: "token"
      }),
      ...mapGetters({
        tokenReverse: "tokenReverse"
      }),
      ...mapState("products", {
        iphone: "iphone"
      })
      // userName() {
      //   return this.$store.state.userName;
      // },
      // token() {
      //   return this.$store.state.token;
      // },
      // tokenReverse() {
      //   return this.$store.getters.tokenReverse;
      // }
    },
    methods: {
      handleChange(e) {
        console.log("e :", e);
      },
      ...mapMutations("products", {
        setAmount: mutations => {
          mutations(SET_PRODUCTS_MOUNT, 100);
        }
        // "SET_PRODUCTS_MOUNT"
      })
      // ,
      // setAmount() {
      //   this.$store.commit("products/SET_PRODUCTS_MOUNT", 100);
      // }
    }
  ```

### 2. 使用重点

* state 取值
* setters 获取计算值
* commit 利用mutations的方法更改数据
* dispatch 利用 actions的方法异步更改数据，actions的方法 先进行异步处理，然后利用mutations的方法更改数据
* 模块化，使用时加入命名空间，与路由或者业务模块尽量一致
* mutations 用常量定义

### 3. 特点

1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

