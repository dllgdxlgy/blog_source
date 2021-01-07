---
title: jQuery复习（1）
date: 2020-10-07 13:45:17
tags: 
- jQuery
categories:
- jQuery
---

<center>开始第一天复习jQuery
</center>

<!--more-->

####基础知识

1. $ 或 jQuery是一个函数，既是函数也是对象。

2. $( )返回的对象就是jQuery对象。

3. 文档夹在完成才执行

   ```javascript
   $(function(){ //绑定文件加载完成后的监听
     
     
   })
   ```

   

4. 引入jQuery后，当函数用：$(***)

   当对象用：$.(***)

5. 作为一般函数调用: $(param)
     1). 参数为函数 : 当DOM加载完成后，执行此回调函数
     2). 参数为选择器字符串: 查找所有匹配的标签, 并将它们封装成jQuery对象
     3). 参数为DOM对象: 将dom对象封装成jQuery对象
     4). 参数为html标签字符串 (用得少): 创建标签对象并封装成jQuery对象

   作为对象使用: $.xxx()

   1). $.each() : 隐式遍历数组

   2). $.trim() : 去除两端的空格

6. jQuery对象是一个包含所有匹配的任意多个dom元素的伪数组对象，所谓的伪数组对象就是只拥有数组的属性，例如长度属性、数值下标属性，但是没有数组的方法。

   基本行为
     * size()/length: 包含的DOM元素个数
     * [index]/get(index): 得到对应位置的DOM元素
     * each(): 遍历包含的所有DOM元素

     *index(): 得到在所在兄弟元素中的下标

   ```javascript
   var $btn = $('button');
   console.log($btn.size())
   ```

---

### 选择器

#### 基本选择器


1. 是什么?
  
  - 有特定格式的字符串
2. 作用
  
  - 用来查找特定页面元素
3. 基本选择器

  ​        ‘#’id : id选择器

  - element : 元素选择器
  - .class : 属性选择器
  - *: 任意标签
  - selector1,selector2,selectorN : 取多个选择器的并集(组合选择器)
  - selector1selector2selectorN : 取多个选择器的交集(相交选择器)

#### 层次选择器

层次选择器: 查找子元素, 后代元素, 兄弟元素的选择器

1. ancestor descendant
     在给定的祖先元素下匹配所有的后代元素

2. parent>child
     在给定的父元素下匹配所有的子元素

3. prev+next
   匹配所有紧接在 prev 元素后的 next 元素

4. prev~siblings
   匹配 prev 元素之后的所有 siblings 元素
   -->

   ```javascript
    //1. 选中ul下所有的的span
   $('ul span').css('background', 'yellow')
   
     //2. 选中ul下所有的子元素span
   $('ul>span').css('background', 'yellow')
   
     //3. 选中class为box的下一个li
   $('.box+li').css('background', 'yellow')
   
     //4. 选中ul下的class为box的元素后面的所有兄弟元素
   $('ul .box~*').css('background', 'yellow')
   ```

   

#### 过滤选择器

理解：在原有的选择器上进行进一步筛选

例子：

```javascript
  //1. 选择第一个div
  // $('div:first').css('background', 'red')

  //2. 选择最后一个class为box的元素
  //$('.box:last').css('background', 'red')

  //3. 选择所有class属性不为box的div
  // $('div:not(.box)').css('background', 'red')  //没有class属性也可以

  //4. 选择第二个和第三个li元素
  // $('li:gt(0):lt(2)').css('background', 'red') // 多个过滤选择器不是同时执行, 而是依次
  //$('li:lt(3):gt(0)').css('background', 'red')

  //5. 选择内容为BBBBB的li
  // $('li:contains("BBBBB")').css('background', 'red')

  //6. 选择隐藏的li
  //console.log($('li:hidden').length, $('li:hidden')[0])
  
  //7. 选择有title属性的li元素
  // $('li[title]').css('background', 'red')

  //8. 选择所有属性title为hello的li元素
  //$('li[title="hello"]').css('background', 'red')
```

#### 表单选择器

具体看相关文档

```javascript
<form>
  <input  type="text"    />  
    <input type="radio"  />
</form>
```

```javascript
$(':text')
```

#### 工具方法

1. $.each(): 遍历数组或对象中的数据

2. $.trim(): 去除字符串两边的空格

3. $ .type(obj): 得到数据的类型
4. $.isArray(obj): 判断是否是数组

5. $.isFunction(obj): 判断是否是函数

6. $.parseJSON(json) : 解析json字符串转换为js对象/数组