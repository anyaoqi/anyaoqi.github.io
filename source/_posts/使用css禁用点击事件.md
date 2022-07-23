---
title: 使用css禁用点击事件
date: 2019-11-20 13:43:28
categories:
    - web前端
tags:
    - css
---

js阻止默认行为：` event.preventDefault() ` 或 `return false`
Js阻止事件冒泡： ` evnet.stopPropagation() ` 或  `e.cancelBubble = true` （IE）

# 使用css禁用点击事件   

&emsp;&emsp;在css中有很多实用但平常不常用的属性，比如今天要说的 `pointer-events`属性。这个css属性的作用就是控制标签的事件是否可用，如果在css里面把标签的这个属性值改为none，那么这个标签就失去了任何的事件，也就做到了禁用点击事件的效果，即使在js里面已经绑定过事件也是不可点击的。

### pointer-events 的作用：

1 阻止用户的点击动作产生任何效果

2 阻止缺省鼠标指针的显示

3 阻止CSS里的hover和active状态的变化触发事件

4 阻止JavaScript点击动作触发的事件

示例： 

        .disabled {
            pointer-events: none;
            cursor: default;
            opacity: 0.6;
        }