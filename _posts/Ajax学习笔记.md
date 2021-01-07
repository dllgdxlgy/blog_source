---
title: Ajax学习笔记
date: 2020-10-14 16:00:57
tags:
- Ajax
categories:
- Ajax
---

<center>文案</center>

<center>白天隐藏在入夜的灯，风躺进熟睡人的呼吸</center>

<center>芦苇是地底的云，你推窗望过来，瞳孔是距我最近的星🌟</center>

<!-- more -->

### 工作原理

![image-20201014162325571](https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20201014162325571.png)

完成高功能：局部刷新，但是不可以后退。

使用XMLHttpRequest对象

```java
xhr = new XMLHttpReuqest();
```

xhr拥有一些属性方法，

### 什么是 Ajax？

不用刷新页面，但可以和服务端进行通信的方式，使用Ajax的主要方式是XMLHttpRequest对象

### Ajax 传送数据的3种方式

(1 )xml：笨重，解析困难，但是 xml 是通用的数据交换模式。

(2) html：不需要解析直接放到文档中，若尽更新一部分数据，但传送数据不是很方便，且HTML代码需要拼装完成。

(3) JSON：小巧，有面向对象的特性，且第三方的 jar 包可以把 java 对象或集合转化为 JSON 字符串（用的最多）

### 使用 jQuery 完成 AJAX 操作

(1) load方法：可以用于 HTML 文档的元素节点，把结果直接加为对应的子元素，通常而言，load 方法加载后的数据是一个 HTML 片段，

```javascript
var $obj = ...

Var url = ...

var args = {key:value,...}

$obj.load (url,args);
```

(2). 

```
$.get ,  $post, $.getJSON: 
```

上面这3个方法更加灵活，除去使用 load 方法的情况， 大部分时候都使用这3个方法。





