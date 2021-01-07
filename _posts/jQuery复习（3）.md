---
title: jQuery复习（3）
date: 2020-10-10 16:43:56
tags: 
- jQuery
categories:
- jQuery
---

<center>继续学习~</center>

<!--more-->

1. 关于新添加的元素没有被绑定事件，解决方法：给要绑定的元素的父元素绑定（事件委托）

```javascript
//问题：新添加的元素，点击以后不会变红
<ul>
  <li>11111</li>
  <li>1111111</li>
  <li>111111111</li>
  <li>11111111111</li>
</ul>
<br>
<button id="btn">添加新的li</button>
<br>

$('ul>li').click(function () {
    this.style.background = 'red'
  })

  $('#btn').click(function () {
    $('ul').append('<li>新增的li....</li>')
  })
```

2. 事件委托(委派/代理):
   将多个子元素(li)的事件监听委托给父辈元素(ul)处理
   监听回调是加在了父辈元素上
   当操作任何一个子元素(li)时, 事件会冒泡到父辈元素(ul)
   父辈元素不会直接处理事件, 而是根据event.target得到发生事件的子元素(li), 通过这个子元素调用事件回调函数

   事件委托的2方:
   委托方: 业主  li
   被委托方: 中介  ul

   使用事件委托的好处
   添加新的子元素, 自动有事件响应处理
   减少事件监听的数量: n==>1

   jQuery的事件委托API
   设置事件委托: 

   ```javascript
   $(parentSelector).delegate(childrenSelector, eventName, callback)
   ```

   例子：

   ```js
    $('ul').delegate('li', 'click', function () {
       console.log(this)
       this.style.background = 'red'
     })
   ```

   移除事件委托: 

   ```js
   $(parentSelector).undelegate(eventName)
   ```

3. 淡入淡出: 不断改变元素的透明度(opacity)来实现的
   fadeIn(): 带动画的显示
   fadeOut(): 带动画隐藏
   fadeToggle(): 带动画切换显示/隐藏

   fadeIn()无参数，效果会立刻出现

   fadeIn('slow')字符串参数

   fadeIn(3000)   3秒

   ```js
    $('#btn1').click(function () {
       //$div1.fadeOut()
        //$div1.fadeOut('slow')
       $div1.fadeOut(1000, function () {
         alert('动画完成了!!!')
       })
     })
   ```



