---
title: 小菠萝Pinia快速入门学习
date: 2022-09-24 18:51:17
tags:  
  - pinia
categories: 
  - web前端
---

**Vue3状态管理工具-Pinia快速入门学习**

## 什么是Pinia？

![pinia](img/pinia.png)

pinia是vue3官方的状态管理工具，当然vue2也可以用。vue2中的状态管理工具是vuex，vue3中不再使用vuex，推荐使用的是pinia, 和vuex差不多，但比vuex更方便、更强、更好。所以你也可以把**pinia理解为vuex的升级版**。

Pinia官网链接：https://pinia.vuejs.org/

### Pinia模块

* State
* Getters
* Actions
* Plugins

用过Vuex的人可能会觉得我少写了一个Mutations，我没写错，pinia确实是没有Mutains和modules的。

以前vuex中是有mutains主要是用户不可以直接修改state，但在**pinia中是可以对state直接修改的**，所以也就不需要mutains。

## 在线示例

[点击查看vue3+pinia示例](https://stackblitz.com/edit/vue-pinia?embed=1&file=src/App.vue)

## 下载

GitHub地址：https://github.com/vuejs/pinia

**vue3**

```
npm install pinia
```

> 如果你使用的是vue2除了下载上面的pinia还需要下载一个@vue/composition-api, 执行下面的命令下载，vue3不用。
>
> npm install pinia @vue/composition-api

## 使用

### 1. 创建实例

首先需要在main.js中引入pinia，然后通过导入**createPinia**方法创建pinia实例

**main.js**

```javascript
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const pinia = createPinia()
const app = createApp(App)

app.use(pinia)
app.mount('#app')
```

### 2. 定义Store

* 首先在src目录下面创建`stores`文件夹
* 然后在stores文件夹中创建`count.js`, 文件名称可以随便写。
* 然后在stores/count.js文件中用过**defineStore**进行定义Store

#### Options语法

```javascript
import { defineStore } from 'pinia'

export const useCountStore = defineStore('main', {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubleCount: (state) => {
      return state.count*2
    }
  },
  actions: {
    increment() {
      this.count++
    }
  }
})
```

#### setup语法

> 创建store是有两种写法的，第一种是上面的**Options写法**，另一种是和Vue3中Composition Api写法类似的**setup写法**

```javascript
import { ref, computed } from 'vue';
import { defineStore } from 'pinia'

// Setup写法
export const useCountStore = defineStore('main', () => {
  // State
  const count  = ref(0);
  // getter
  const doubleCount = computed(() => count.value*2)
  // actions
  const increment = function(){
    count.value++
  }

  return {
    count,
    doubleCount,
    increment
  }
})
```

在setup写法中通过**ref**定义state，通过**computed**定义getter，通过**function**定义action

* `ref` = `state`
* `computed`= `getters`
* `function` = `actions`

### 3. 使用store

> 定义好store后就可以在页面使用了，现在介绍一下如何在页面中使用store

**Script**

```javascript
import { storeToRefs } from 'pinia';
import { useCountStore } from './stores/count';

export default {
  name: 'App',
  components: {},
  setup() {
    const store = useCountStore();
    const { increment } = store;
    const { count, doubleCount } = storeToRefs(store);

    return {
      count,
      doubleCount,
      increment,
    };
  },
};
```

> 下面是代码解读

1. 从/stores/count.js中导入定义的useCountStore

2. 从store中解构出increment方法

3. 如果**直接从store中解构state会失去响应性**，也就是改了state页面上显示的state不会改变。所以需要使用**storeToRefs**方法将store中的state转为ref再进行解构，这样修改数据页面上也就会跟着变了。

   ```javascript
   import { storeToRefs } from 'pinia';
   ```

   ```javascript
   const { count, doubleCount } = storeToRefs(store)
   ```

**template**

```vue
<div>
  <p>count: {{ count }}</p>
  <p>doubleCount: {{ doubleCount }}</p>
  <button @click="increment" > increment </button>
</div>
```


