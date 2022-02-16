---
title: ES6
date: 2021-7-23
tags:
 - tag4
categories: 
 - JS-node
---

# ES6

#### 严格模式 ”use strict“

注意：在严格模式中：

1.未定义不能使用

2.函数与变量不能同名

3.函数不能出现同名参数

4.不能使用with（）{}语法

5.不能修改只读属性

6.不能使用八进制

7.不能删除不可删除属性

8.不能在它的外层作用域引入变量eval

9.eval和arguments不能被重新赋值

10.arguments.callee和arguments.callee.caller不能使用

11.禁止this指向全局对象，顶层的this指向undefined，即不应该在顶层代码使用this

设置只读属性：

```javascript
var obj={a:1,b:2}
Object.defineProperty(obj,"c",{
	writable:false,
	value:3
})// 说明在obj对象上添加了一个只读属性c
```

设置不可删除属性

```javascript
var obj={a:1,b:2}
Object.defineProperty(obj,"c",{
    configurable:false,
    valse:6
})// 表示在obj对象中设置了一个不可删除属性c
```

回调函数与函数直接调用时，this指向一致，在ES5非严格模式中指向window，则严格模式中，指向undefined；其中setInterval()和setTimeout()特殊，在任何情况下都指向window

#### let和const

let：作用域为当前块语句的内部，**let不存在变量提升（预解析）**

var定义变量时，会定义为window的属性

let定义时，不会

const：定义常量，不能被修改

```javascript
var temp=123
if(true){
	temp="abc" // 报错，不能在变量定义let定义之前赋值；因为let没有预解析
	let temp
}
```

#### 箭头函数

箭头函数最终的目的是解决 **this指向问题**

箭头函数是匿名函数

var fn=()=>{}

var fn=item=>{}

var fn=(a,b)=>{}

var fn=(a,b)=>a+b

使用函数和执行函数时，this都会被改变

**箭头函数语句块内的this指向当前箭头函数外上下文环境的this**

**谁执行了函数，函数中的this就指向谁**

箭头函数中没有arguments

如果需要删除这个侦听，必须把箭头函数存储在一个属性上，然后后面调用并删除

#### 解构赋值

1.数组赋值

var arr=[1,2,3]

var [a,b,c]=arr //将数组中的元素按照顺序赋值给a,b,c三个变量

a,b,c分别是1,2,3 三个都是全局变量

a=3,b=4     [a,b]=[b,a] //将a,b的值交换

2.对象解构：按key解构，没有顺序

var obj={a:1,b:2,c:3}

var {b,a}=obj // a=1,b=2

var obj={a:1,b:2,c:{d:20}}

var {a,b,c:{d}}=obj //a=1,b=2,d=20 c只是一个中间过渡的，没有具体值，若要查看则会报错

var {a:1,b:2,c:{a:4,b:5}}

var {a,b,c:{a:a1,b:b1}} // a=1,b=2,a1=4,b1=5

解构时的冒号就是起别名

解构时的等号就是赋初值

var {max,min,random}=Math

实例对象拆解时，不能拆解实例化方法，只能拆解实例化属性，静态属性和静态方法

var obj={a:1,b:2,c:3}

var o={...args}  // o={a:1,b:2,c:3}

function fn(**...[a,b]**){

​	console.log(a,b)  //3,4   **fn(3,4)**

}

function fn(**[a,b]**){

​	console.log(a,b) //3,4 **fn([3,4])**

}

解构时尽量不要使用小括号

#### Symbol

就是一个永远不重复的值；作为对象的key使用，让key唯一

对象的属性key可以是string或者Symbol

对象中的Symbol不能被for..in.. 遍历

#### Set和Map

Set：无序的不重复的集合；松散解构；只是用于存储值的；没有键名；不能排序；不重复

属性和方法：

1.size ：集合元素的数量，只读

2.add() ：添加元素

3.delete() ：删除

4.clear() ：清空

5.has() ：判断有没有

6.forEach(function(item){}) ：遍历

作用：

1.数组去重

arr=Array.from(new Set(arr))

2.for..of..遍历

var s=new Set([1,2,5,3,7])

for(var value of s){

​	conole.log(value)

}

Map：类似于HashMap，也是一个键值对;**以引用地址来存储**

属性和方法：

1.set(键，值)

2..get(键)

3.has(键) 判断有没有

4.delete(键) 删除

5.clear() 清空

6.size 属性

以对象存储值

var  m=new Map()

```javascript
for(var [key,value] of m){}
```

```javascript
.forEach((item,key)=>{})
```

```javascript
for(var key of m.keys()){} //只遍历所有键
```

```javascript
for(var value of m.values()){}  //只遍历所有值
```

```javascript
for(var [key,value] of m.entries()){}
for(var [key,value] of m){}//是上面的简写
```

```javascript
var arr=[1,2,3,5,6]for(var value of arr){}for(var [key,value] of arr.entries()){}//跟上面的效果一样
```

对象不是迭代器，所以不能使用for..of遍历

将迭代器转换为对象

obj=Object.fromEntries(m)

将对象转换为迭代器

m=Object.entries(obj)

所以：将对象转换为Map

var obj=new Object()

var arr=new Map(Object.entries(obj))

#### 弱引用

WeakSet：里面只能使用引用类型

WeakMap：里面只能使用引用类型做key

强引用时，如果其他有引用时，设置null时，不能被清除

弱引用时，可以被清除

#### 生成器函数

是一个迭代器

yield(断电) 支持for...of...遍历

方法：

1.next() 下一步

2.return() 

3.throw()

状态机：suspected     closed

#### 类

不是抽象化的

new 类名() //实例化类 ；执行类中的constructor，类中constructor与类名相等

constructor中的this指实例化的对象

方法中的this指的是谁调用这个方法，this就是谁

static静态

静态方法中的this（一般不写）和实例化对象的this（实例化对象）不一致

只要能找到类的地方都可以直接调用静态方法

实例化方法必须通过实例化后的对象调用

#### 继承

基类：JS所有基类都是Object

超类：子类的父类，直接继承

父类

子类

因为子类继承超类，所以在实例化子类的时候就自动执行了超类的构造函数

如果重写了构造函数，意味着脱离了原有继承执行的构造函数，这样写违背了继承的基本思路（必须要执行超类构造函数）

super()执行超类的构造函数

只要在子类重写构造函数，第一句必须写super（参数），一旦没有执行构造函数，直接使用this就会报错，因为这个时候还没有继承

继承后覆盖override 方法重写

如果希望先执行超类中的方法内容，在执行新内容之前，使用super.方法（），此时的super相对于超类中的this，这样类似于叠加或扩展方法的内容。

### cmd/amd

- AMD 是 RequireJS 在推广过程中对模块定义的规范化产出
- CMD是SeaJS在推广过程中对模块化定义的规范化产出

这两种规范是服务于JavaScript的模块化开发，目前两种都能实现浏览器端的**模块化开发的目的**，不同之处是**CMD是懒执行,AMD是预执行**

##### 他们的区别是

1. 对于依赖的模块，AMD是提前执行，CMD是延迟执行。不过RequireJS从2.0开始，也改成了可以延迟执行（根据写法不同，执行的方式不同）

2. CMD推崇就近依赖，AMD推崇依赖前置

3. AMD支持全局require、局部require，但是CMD不支持全局require，所以CMD没有全局API而AMD有

   ```javascript
   //AMD的方式define(['./a','./b'],function(a,b){a.dosmting();//省略1W行b.dosmting();})//CMD的方式define(function(require,exprots,module){var a = require('./a');a.dosmting();//省略1W行var b = require('./b');b.dosmting();})
   ```

**注意**：在HTML页面引入时，需要

```javascript
<script src="./require.js" data-main="./Main"></script>// src里面必须导入require包// data-main里面写我们想要导入的js文件
```

