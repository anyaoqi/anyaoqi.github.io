---
title: 前端面试总结--JS篇
date: 2022-09-18 18:20:15
tags: 
  - 面试
categories: 
  - web前端
---


#### 数据类型

**js数据类型有哪些？**

* 基本数据类型：Number、Boolean、String、Null、Undefined、Symbol(ES6)、bigInt
* 引用数据类型：Object、Array、Function、RegExp、Date

#### 闭包

**什么是闭包** 

​	闭包就是在函数内可以访问其他函数内的变量
​	可以通过在函数内返回函数实现

​	缺点：比较耗费内存、使用不当会造成内存溢出的问题

#### 作用域

**局部作用域、全局作用域的区别**

、	局部作用域就是大括号内的区域，在此区域内可以访问定义的变量。
​	全局作用域就是在任何地方都可以访问的区域，例如使用var定义的变量

#### 堆栈

**对栈和堆的理解**

​	栈内存：存储基本类型，[Boolean](https://so.csdn.net/so/search?q=Boolean&spm=1001.2101.3001.7020)、Number、String、Undefined、Null。变量赋值时，赋值的是变量本身。
​	堆内存：存储引用类型，Function，Array，Object，将变量赋值时，赋值的是指针，不是变量本身。

#### 原型、原型链、继承

**对原型、原型链的理解**

​	任何一个**普通函数、类**的身上都有**prototype**属性，**prototype**指向的就是该对象的原型。

​	当访问一个对象的属性时，首先会在当前对象的属性上查找，如果没有找到就会去对象的原型上面再找，如果原型的属性上也没有要找的属性就再找这个原型的原型上面的找，直至找到window上。

#### 浅拷贝、深拷贝

**什么是浅拷贝和深拷贝？**

* 浅拷贝：只会赋值一层，当对一个变量进行赋值的时候，赋值的只是对象的指针，不是对象本身的值，修改这个变量的时候之前的对象也会有影响，这样的赋值就是浅拷贝。浅拷贝基本数据会复制变量的值，引用类型会赋值对象的指针。
* 深拷贝：多层赋值，当对一个变量进行赋值的时候，赋值的是对象的值，不会赋值对象的指针，修改当前变量的时候不会对影响之前对象。

**如何实现浅拷贝？**

* 普通for循环遍历

* Object.assign

**如何实现深拷贝？**

​	通过递归实现，在递归里面生成一个新的对象，然后把原来对象上的属性都赋值给新对象属性上。  

```javascript
function deepClone(obj){
  if (typeof obj !== 'object' || obj == null){
    return obj;
  }
  let result;
  if (obj instanceof Array){
    result = []
  } else {
    result = {}
  } 
  for(var key in obj) {
    if (obj.hasOwnProperty(key)){
      result[key] = deepClone(obj[key]);
    }

  }
  return result;
}
```



#### 事件流

**什么是事件流、事件冒泡？**

​	当点击一个元素时，事件的发生是有一个过程的，这个过程一共分为三个阶段，分别为：捕获阶段、目标阶段、冒泡阶段。

​	捕获阶段：从最外层向下遍历dom，一层一层进行捕获对应的事件，一直到最终的目标dom。

​	目标阶段：当捕获阶段完成后就到达了目标元素上面，触发目标元素的对应事件。

​	冒泡阶段：目标元素事件触发完成后，开始触发dom父级的对应事件。

**如何取消事件冒泡？**

```
event.stopPropagation()   // 非IE

window.event.cancelBubble = true;  // IE的方式来取消事件冒泡
```

**如何阻止事件默认行为？**

```
event.preventDefault()
```

#### this指向，修改指向方法

**this指向的理解**

​	默认this指向的是window

​	构造函数中的this指向当前对象

​	绑定事件函数里面的this指向函数的调用者

**箭头函数this指向的是什么？**

​	箭头函数中的this指向函数外部的this

#### call, alpay,bind的区别

* 作用相同，都是可以改变this指向

* call和appaly是直接执行该函数，bind方法执行后返回该函数，需要再多加一个()执行。
* 第一个参数都是this的指向对象, 第二个参数call和bind是挨个放进去，apply是数组

#### cookie、localStorage、seccionStorage的区别

**cookie、localStorage、seccionStorage的区别**

* 一、存储的时间有效期不同

​	cookie有效期可以设置，默认的情况下是关闭浏览器后失效。
​	sessionStorage有效期是保持在当前页面,关闭当前会话或者浏览器后会失效
​	localStorage的有效期是长期的，如果不手动删除会一直有效。

* 存储的大小不同

​	cookie的存储大小是4kb，存储量小。

​	localStorage和sessionStorage的存储大小是5M，存储量大。

* 与服务端的通信

​	cookie可以参与到与服务端的通信中，在请求中可以把cookie带到后端。

​	localStorage和sessionStorage是单纯的前端存储，不参与与服务端的通信

#### ---Promise

​	Promise主要是为了解决ajax链式调用的问题，

​	通过new Primise创建promise，接收一个构造函数，通过resole和reject返回成功或失败的结果。

​	通过.then方法再执行后续的内容，通过.catch捕获错误。



#### var、let、const区别

const和let是局部作用域，var是全局作用域。

cosnt定义的数据是常量，不允许修改。let和var定义的是变量，可以修改。



#### ---对象

* 工厂模式
* new Object
* 原型模式
* {}
* 构造函数



#### 事件循环机制，宏任务、微任务

> 任务、微任务、队列和时间表: https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/

**js代码执行的流程是怎样的？**

* js代码执行流程：同步代码先执行完 > 进入**事件循环机制**开始执行异步代码(宏任务和微任务)

**JavaScript 是单线程，如何执行异步代码？**

* 通过**事件循环机制**执行异步代码

**什么是js事件循环机制？**

* 事件循环机制： **事件循环分为微任务和宏任务，先执行微任务，然后dom渲染，再执行宏任务**
  * 微任务(microtasks)：Promise、 
  * 宏任务(macrotasks)：setTimeout、setInterval

**如何手动创建一个微任务事件？**

* 创建一个微任务：queueMicrotask

  > queueMicrotask: https://developer.mozilla.org/zh-CN/docs/Web/API/queueMicrotask

  ```javascript
  console.log("a");
  queueMicrotask(() => {
    console.log("b")
  });
  console.log("c");
  
  结果：
  a
  c
  b
  ```

**打印结果是什么？几秒打印几？**

```javascript
for(var i=0; i<=3; i++){
   setTimeout(function(){
   		console.log(i)
   }, 1000*i)
}

3
3
3
```

每隔一秒打印一个3


**事件循环机制面试题**

```javascript
console.log('script start');

setTimeout(function () {
  console.log('setTimeout');
}, 0);

Promise.resolve()
  .then(function () {
    console.log('promise1');
  })
  .then(function () {
    console.log('promise2');
  });

console.log('script end');
```

#### 