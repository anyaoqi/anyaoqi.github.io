---
title: 前端面试题-Vue
date: 2023-04-08 22:34:05
categorie: 面试题
tags: Vue面试题
---

### MVVM的理解

**Model 模型， View  视图，ViewModel 视图模型**

### v-show和v-if的区别

**v-show控制样式display隐藏显示**

**v-if控制是否渲染dom**

### for循环中key的作用

**  循环项增加指针，提高性能**

### watch、computed、methods区别

**watch是监控某个数据的变量，当数据变化的时候执行其他的操作。**	**`immediate`**添加属性可以在第一次调用时执行，`deep`进行深度监听

**computed 是根据依赖的数据变化，让本身的数据发生变化**

**methods 是定义的方法，可以在执行的时机执行**

### Vue生命周期

* **beforeCreate  不能访问this**
* **created  有this**
  * **请求数据  如果有涉及dom的操作要放到nextTick中**
* **beforeMounte**
* **mounted**
  * **操作dom**
* **beforeUpdate**
* **updated**
* **beforeDestory  （Vue3:unMounte）**
* **Destoryed    （Vue3:unMounted）**
* **deactivated（keep-alive离开）**
* **activated（keep-alive进入）**

### Vuex状态管理

* **五个模块：state、getters, mutions, actions,  mudules**
* **在actions中执行异步操作，然后通过commit执行mution，在mution中修改state的值，在页面中通过computed计算属性引用。**
* **mapGetter、mapActions**

### 改了数据页面没有变

**由于JavaScript的限制，Vue不能检测数组和对象属性的删除和增加**

**使用官方提供的** `$set`方法

### Keep-alive

**用来做组件缓存，当切面需要频繁切换的时候不想让内容每次都加载恢复到初始的样子，可以使用keep-alive进行缓存**

**使用keey-alive包裹路由组件，通过exclude排除页面，include白名单包含要缓存的页面。**

### next-Tick

**dom更新完毕后执行**

**原理：首先使用Promise, 如果不支持Promise使用MutationObserver，都不行最后会使用setTimout**

### data为什么是函数

**通过函数返回一个新的对象，等于每个组件都是单独的data对象，如果data是对象的话所有组件都会同步。**

### Vue2、Vue3响应式原理

**Vue2**

**通过Object.definePrototype**

**Vue3**

**通过proxy**

### Vue父子组件通信

* **父->子：Props  **
* **子->父：$emit**
* **子->父：$parents**
* **父->子：$ref**

### Vue非父子组件通信

* **桥接  子1->父->子2**
* **eventBus**
* **深层：父provide/子inject（Vue2.2.0）**
* **Vuex**

### Vue-router路由模式和实现原理

* **hash模式   window.onhashchange      **
* **history模式  history.pushState   需要后端配合将请求指向index.html，否则会404**

### Vue-router路由生命周期

**路由钩子**

**全局钩子：进入之前：beforeEach、解析中：beforeResolve、进入之后：afterEach、**

**单个路由：beforeEnter**

**组件路由：进入之前：beforeRouteEnter、更新：beforeRouteUpdate、离开之前：beforeRouteLeave**

**执行顺序**

* **上一个组件离开->先全局 -> 再单独 -> 最后组件内**
* **组件离开之前 -> 全局进入之前 -> 单独路由进入之前 -> 组件内进入之前 -> 全局解析中 -> 全局进入后 -> 组件内进入后**

1. **beforeRouteLeave - 组件离开**
2. **beforeEach - 全局进入**
3. **beforeEnter - 单独路由进入**
4. **beforeRouteEnter - 组件进入**
5. **beforeResolve - 全局解析**
6. **afterEach - 全局进入后**
7. **beforeRouteEnter - 组件进入后**

### Vue虚拟DOM

**虚拟dom组成结构为标签名称tagName、标签属性props、标签子元素children**

```
let element={
    tagName:'ul',//节点标签名
    props:{  //dom的属性，用一个对象存储键值对
        id:'list'
    },
    children:[//该节点的子节点
        {tagName:'li',props:{class:'item'},children:['aa']}，
        {tagName:'li',props:{class:'item'},children:['bb']},
        {tagName:'li',props:{class:'item'},children:['cc']}
    ]
} 
```

## Vue3

### Vue3有哪些更新

* **componstion Api-组合式API**
* **Object.defineProperty改为proxy**
* **对Ts更好的支持**
* **framents-根组件支持多节点**
* **Teleport-可以将dom移动到指定位置**
* **script setup**

### Vue3 Componstion Api

**更方便逻辑重用，逻辑更清晰，相同功能逻辑放到同一个hook中**

### reactive和ref有什么不同？

**reacive是一组数据，传入对象，使用的时候也不需要通过.value**

**ref适合基础数据，使用的时候需要通过.value**

### 说一下Vue3中的tree shaking特性

**去除掉没有使用过的代码，vue3中会检测在项目中使用了那些功能，没有使用过的将不会打包。**

### Vue2和Vue3中diff算法的区别

**Vue2是全量更新，Vue3中是静态标记+非全量更新**

**修改当前组件中的某个属性会更新整个组件，Vue3中只会修改对应的dom**
