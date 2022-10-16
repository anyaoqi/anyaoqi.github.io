---
title: HTML如何修改placeholder属性中文字颜色
date: 2022-10-16 20:36:11
tags:
cagegoryes: 
    - 踩坑之路
---

​		今天在群里看到群友问了一个这样的问题，就是如何更改placeholder属性中文字的颜色，以前用过这属性，却是没更改过颜色，于是便试了试，中途遇到些问题，查找资料后特来总结一下。

　　熟悉HTML5的人应该都知道，placeholder这个属性是HTML5中增加的属性，该属性的作用是规定可描述输入字段预期值的简短的提示信息，该提示会在用户输入之前显示在输入字段中，会在用户输入字段后消失，有些浏览器则是获得焦点后该提示便消失（如Safari、IE）

适用范围：placeholder 属性适用于下面的 input 类型：text、search、url、tel、email 和 password。

因为是HTML5中新增的属性，所以会存在兼容性问题。下面说说浏览器的支持情况：

IE10+、Firefox、Opera、Chrome 和 Safari 均支持 placeholder 属性。IE9及以下版本不支持input的placeholder属性。

placeholder的用法，举例：

```html
 <input type="text" placeholder="请输入您要搜索的内容！"> 
```

效果：

![img](https://img-blog.csdnimg.cn/20190216192603232.png)

该提示文字会有自己默认的颜色，然而有时候，我们并不希望用该默认颜色，而是想自定义颜色。那么该怎么处理呢?不废话，上代码。　

```css
<style>
        input::-webkit-input-placeholder{
            color:red;
        }
        input::-moz-placeholder{   /* Mozilla Firefox 19+ */
            color:red;
        }
        input:-moz-placeholder{    /* Mozilla Firefox 4 to 18 */
            color:red;
        }
        input:-ms-input-placeholder{  /* Internet Explorer 10-11 */ 
            color:red;
        }
</style>
```

针对不同浏览器或不同版本的浏览器会有不同的写法，会添加相应的前缀。

　　注意：

　　1、WebKit, Blink, Edge浏览器等需要带上-webkit-前缀，且是双冒号，写的时候还要带上input

　　2、针对火狐浏览器则有两种写法，一种是针对低版本的，一种是针对高版本的，二者都需要带上-moz-前缀。要点1：火狐低版本的使用冒号（：），而高版本的使用双冒号（：：）；要点2：火狐浏览器不需要像webkit内核那样要带上input。

　　3、由于placeholder属性只在IE10+才支持，因此，针对IE10、IE11的写法是加上-ms-前缀，使用的是冒号（：），需要带上input

