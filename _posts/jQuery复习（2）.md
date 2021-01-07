---
title: jQuery复习（2）
date: 2020-10-08 16:50:12
tags: 
- jQuery
categories:
- jQuery
---

<center>赶快来学习～～</center>

<!--more-->

1. 选择p标签的第一个元素，并且把它的样式设置为红色

   ```javascript
   $('p:first').css('color'，'red')
   ```

2. 选的是第二个p元素，这里设置了样式。

   ```javascript
   $('p:eq(1)').css('background','blue')
   ```

3. 内容尺寸
     height(): height
     width(): width
   内部尺寸
     innerHeight(): height+padding
     innerWidth(): width+padding
   外部尺寸
     outerHeight(false/true): height+padding+border  如果是true, 加上margin
     outerWidth(false/true): width+padding+border 如果是true, 加上margin

4. 在jQuery对象中的元素对象数组中过滤出一部分元素来

   ```javascript
   first()
   last()
   eq(index|-index)
   filter(selector)
   not(selector)
   has(selector)
   ```

5. 在已经匹配出的元素集合中根据选择器查找孩子/父母/兄弟标签

   ```java
   children(): 子标签中找
   find() : 后代标签中找
   parent() : 父标签
   prevAll() : 前面所有的兄弟标签
   nextAll() : 后面所有的兄弟标签
   siblings() : 前后所有的兄弟标签
   ```

6. 添加/替换元素
     append(content)
       向当前匹配的所有元素内部的最后插入指定内容

   ```javascript
     var $ul1 = $('#ul1')
     //$ul1.append('<span>append()添加的span</span>')
     $('<span>appendTo()添加的span</span>').appendTo($ul1)
   	//这两种方法都可以
   ```

    prepend(content)
       向当前匹配的所有元素内部的最前面插入指定内容
    before(content)
       将指定内容插入到当前所有匹配元素的前面
    after(content)
       将指定内容插入到当前所有匹配元素的后面替换节点
   replaceWith(content)
       用指定内容替换所有匹配的标签删除节点
   删除元素
   empty()
       删除所有匹配元素的子元素
   remove()
       删除所有匹配的元素

   ```javascript
   $('#ul2>li').remove() // 移除id为u12下的所有li元素
   ```

7.  事件绑定(2种)：

   1. eventName(function(){})

      ```javascript
      $('#div').click(function(){});
      ```

   2. on(eventName, funcion(){})

      ```javascript
      $('#div').on('click', function(){})
      ```

   优缺点:
       eventName: 编码方便, 但只能加一个监听, 且有的事件监听不支持
       on: 编码不方便, 可以添加多个监听, 且更通用

8. 区别mouseover与mouseenter

   mouseover: 在移入子元素时也会触发, 对应mouseout

   mouseenter: 只在移入当前元素时才触发, 对应mouseleave

   hover()使用的就是mouseenter()和mouseleave()

