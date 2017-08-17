---
title: "JavaScript"
date: 2017-08-08 12:04
updated: 2017-08-08 12:04
tag: JavaScript
log: "html中的JavaScript"
---

[TOC]

## 在HTML中使用JavaScript

`<script>`元素：

* async 属性：应立即下载脚本，但不妨碍其他操作，是一种一部的执行下载。仅对外部文件。该属性应该表示为`async`。（XHTML中表示为`async="async"`）

* defer属性：表示在文档被加载完毕之后再对于脚本的加载，样例与将`<script>`标签放置在文档末尾是一致的，仅对于外部文件。该属性表示为`defer="defer"`

* 无论包含那种代码，只要不存在`defer` 和` async`就会按照文档的顺序一次解释执行，当然将`<script>`标签放置在末尾不失为一种好的方法。

* 注释hack：用于JavaScript不被使用的情况下

```html
  <script><!--				以此注释以下的function javaScript语句
   	function sayHi(){
        alert("hi");
   	}
  //--></script>				以此注释结尾标签
```

  `<noscript>`元素：

  出现在不支持 JavaScript 或者禁用JavaScript的情况下

```html
  <noscript>
  	<p>本页面需要启用（支持）JavaScript</p>
  </noscript>
```

## 基本认识

严格模式：ECMAScript 5 中引入，需要在顶部添加代码`use strict;`这个可以加在整个js文件的开头，也可以加在function函数的开头，表示一个局部范围内的严格模式。

推荐使用每一个子语句都要用`{}`语句块隔开，更加的清晰。

var的使用：

```javascript
  var m = "hi";
  m = 100;		//这是可以的

  function m(){
    var me = "hi";	//局部变量
  }

  function m(){
    me = "hi";
  //全局变量。不过如果不调用这个函数，就不会创建这个全局变量（略有差别）但不推荐，不便于管理
  }
```

五种基本数据类型：

* Undefined——未定义
* Null——空
* Boolean——布尔值true false
* Number——数值
* String——字符串

一种复杂数据类型：

* Object

`Null==Undefined` True

`Null===Undefined`False

true 不一定等于1，false不一定等于0。以下为转换法则：

|   数据类型    |    true     |   false   |
| :-------: | :---------: | :-------: |
|  String   |     非空      |    ""     |
|  Number   | 非0;Infinity |   0,NaN   |
|  Object   |    任何对象     |   null    |
| Undefined |     不适用     | undefined |

```
var m = 070;	//开头为0 八进制字面量	严格模式下没有这种说法
var n = 0x1f;	//开头0x 十六进制字面量
```

0.1+0.2=0.3000000000000004 浮点数计算误差。

Infinity 无法参与计算。Number.MIN_VALUE 和Number.MAX_VALUE。

NaN!=NaN NaN 与自身也不相等。

数值转换——Number：

* Boolean->1,0
* null->0
* undefined->NaN
* String
  * "011"->11
  * ""->0
  * 其余->NaN

parseInt(args1,args2)，args1表示数值，args2表示进制。

toString(args)，args可以表示进制。

转换成字符串可以偷懒+""。

Object原生属性、方法：

+ `constructor`：构造方法`Object()`
+ `hasOwnProperty("propertyName")`：对象实例是否有属性，字符串形式指定。
+ `isPrototypeOf(Object)`：是否是当前对象的原型。
+ `propertyIsEnumerable`：关系到是否可用for-in。
+ 其他。

!!  与  Boolean 的效果一致。

关系运算符：

``` javascript
var result = "23" < "3";		//true
var result = "23" < 3;		//false
```

for-in语句：

```javascript
for (var proName in window){
  document.write(proName);
}
```

with语句：

```javascript
with(location){
  var qs = search.substring(1);
  var hostname = hostname;
  var url = href;
}//语句都省略location前缀，但是大型项目不推荐。	
```

arguments的属性实现的方法重载：

```javascript
function add(){
  if(arguments.length == 1){
    alert(arguments[0]);
  }
  else if(arguments.length == 2){
  	alert(arguments[0]+arguments[1]);
  }
}
add(1);		//11
add(1,2);	//3
```

## TODO

*  第四章 变量与作用域