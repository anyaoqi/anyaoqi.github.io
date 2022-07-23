---
title: vue-cli3 项目使用postcss-pxtorem解决移动端适配的问题
date: 2019-11-18 08:39:11
categories: 
        - web前端 
tags:
        - 移动端适配
---
## 一. 项目中引入lib-flexible

lib-flexible 会自动在html的head中添加一个meta name="viewport"的标签，同时会自动设置html的font-size为屏幕宽度除以10，也就是1rem等于html根节点的font-size。假如设计稿的宽度是750px，此时1rem应该等于75px。假如量的某个元素的宽度是150px，那么在css里面定义这个元素的宽度就是 width: 2rem。

1. 安装 lib-flexible 

        npm install lib-flexible --save

2. 在 main.js 中引入

        import "lib-flexible";

## 二. 项目中引入 postcss-pxtorem

postcss-pxtorem: postcss的一个插件，主要是帮你把px转换成对应的rem；
然后：还要用js代码去动态算根目录应该有的字体大小，反正就是一段js代码去动态获取屏幕宽度！

1. 安装 postcss-pxtorem

        npm install postcss-pxtorem -D 

2. 在vue.config.js 中配置 

    首先引入 postcss-pxtorem  

        const pxtorem = require("postcss-pxtorem");
    
    然后在module.exports.loaderOptions.postcss.plugins里面增加以下内容

        pxtorem({
          rootValue: 37.5,
          propList: ["*"]
        })



 好了，现在从F12控制台审查元素看一下你的px有没有自动转换为rem，如果单位是rem说明成功了。
    