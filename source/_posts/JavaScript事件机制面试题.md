---
title: JavaScript事件机制面试题
date: 2019-11-18 08:39:11
categories: 
        - web前端 
tags:
        - 事件机制
        - 面试题
---

## JS事件处理机制/微任务和宏任务

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