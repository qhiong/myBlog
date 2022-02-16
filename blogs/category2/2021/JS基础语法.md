---
title: JS基础语法
date: 2021-2-16
tags:
 - tag4
categories: 
 - JS-node
---

# JavaScript基础知识

1.定义：JavaScript是一个弱类型，解释型语言。

```javascript
&nbsp;字宽空格，容易受字体影响
&ensp;半角空格，1/2个中文宽度，不受字体影响
&emsp;全角空格，1个中文宽度，不受字体影响
```

### 变量

早期所有的变量都是window的属性

当调用window的属性和方法时一般可以省略window

后来改用var 定义来区分是变量还是window的属性

ES6以后禁止将window属性和变量绑定，严格模式和模块开发将会抵制这种写法

**变量命名**

1、变量名必须字母或者下划线或者$起头，不能以数字或其他符号起头

2、变量名不能使用关键词和保留字,不能与window属性和方法同名

3、变量使用驼峰式命名getObjectName,如果是临时变量或者参数可以使用 _起头  例如 ： _name

4、变量命名和常量命名区分变量命名不使用全部大写，常量命名必须使用全大写，_区分  EVENT_ID 

​	注意：常量不能重新赋值，定义后不能改变

```javascript
var a=1;
    {
        a=4;
        function a(){

        }
        a=5;
        function a(){

        }
        a=6;
        function a(){

        }
        a=7;
        console.log(a,"_______") // 7'_______'
    }
console.log(a);// 6

```

### 数据类型

##### 5种基础类型和1种复杂类型

string

number

boolean

undefined

null

Symbol (ES6)

0bject

##### 单引号，双引号，反引号的区别

1.单引号，双引号中不能换行

2.单引号，双引号中不能解析变量

​	**反引号可以解析变量**

​		在反引号中使用***${变量}***来包裹变量会解析变量输出变量中存储的数据，还可以执行计算表达式

```javascript
undefined:
var a;//开辟一个空间，定义这个空间，如果这个空间已经开辟，沿用以前的结果，如果没有开辟，开辟这个空间
var w = undefined;//开辟一个空间，起名为w,不管以前有没有相同的名称空间，全部赋值为undefined
null:
//空值，实际上null的类型属于对象型
var a = null;//主要用于清除对象的应用关系，更新引用关系列表--》对象的时候详说
```

##### undefined和null的区别：

undefined:一般用于定义时使用，做起始未赋值的标识

null:作用是清楚引用关系，所以只用于赋值为对象的变量清空。

##### typeof()：用于判断变量值的类型

### 数据类型的转化

#### 1.所有类型转化为字符串：

**a.强制转换法**：所有**隐式转换**都使用强制转换法（构造函数转换法）

**注意：**

1. 所有对象转换为字符串时都是[object object]
2. 所有对象的属性如果不是字符串，都会隐式转换为字符串
3. 所有数组强制转换为字符串，结果会将数组中的所有值用逗号隔开的字符串形式。

**b.toString() 方法**

1. 将其他数值转换为字符串类型
2. 加参数（2~36之间的整数）：会将数值转换为字符串进制，参数为小数时，会向下取整floor

**c.toFixed()：**保留几位小数，并且四舍五入

**d.+=“”加等一个空的字符串**

##### String和toString()的区别

toString()没有办法转换null和undefined，转换就会报错

String转换null和undefined就直接转换

#### 2.将任何内容转换为数值

**a.强制转换法**：Number(),也称构造函数转换法（隐式转换）

```javascript
	var a="10";//10
    var a="10a"; //NaN  非数值
    var a="";//0
    var a='a10';//NaN
    var a=true;//1
    var a=false;//0
    var a=undefined;//NaN
    var a=null;//0;
    var a={a:1};//NaN

    // 数组转数值时，先转换为字符串，再转换为数值
    var a=[1,2];//NaN
    var a=[1];//1
    var a=[];//0
```

**b.parseInt() 按进制转换整数**

```javascript
var a = '10a' //10
var a = 'a10' //NaN
var a = true //NaN  ---> 因为true不是字符串，所以会先将true隐式转换为字符串，然后再转换为数值，‘true’无法当作数值，所以转化结束为NaN
```

​	parseInt(参数1，参数2)还可以按进制转换为整数

​	参数1：要转换的值

​	参数2：进制（把 参数1 当作 参数2 进制字符串转换为十进制）

```javascript
var a = 'FF' //parseInt(a,16) ->255
```

**c.  parseFloat() 转换为十进制小数**

```javascript
var a = '12.34' //12.34
```

#### 3.所以类型转换为布尔值

“” 0 false null undefined NaN 强制转换都是false

其他所有转换都为 true

#### 4.所有类型转换为对象

字符串、数值、布尔值转为对象为字符串、数值、布尔值对象

### 为什么要使用href=" javascript:void(O);"

javascript是伪协议。表示url的内容通过javascript执行。 void(0)表示不作任何操作，这样会防止链接跳转到其他页面。这么做往往是为了保留链接的样式，但不

让链接执行实际操作，

```javascript
<a href="javascript: void(0)" onClick="window.open()">点击链接后，页面不动，只打开链接
<a href="#" onclick="javascript:return false;">作用一样，但是不同浏览器会有差异
```

**href=" javascript:void(0);”与href=”#"的区别**

```javascript
<a href- "javascript.void(0)">点击</a> //点击链接后不会回到网页顶部<a href="#">点击</a> //点击后会回到网面顶部"#"其实是包含了位置信息，例如默认的锚点是 #top 也就是网页的上端//而javascript:void(0)仅仅表示一个死链接这就是为什么有的时候页面很长浏览链接明明是#可是跳动到了页首//而javascript:void(0)则不是如此所以调用脚本的时候最好用void(O)
```

#### isNaN()和Number.isNaN()和Object.is()

isNaN():判断是否是数值

Number.isNaN():判断是否是数值，然后判断是否是数值型的NaN

```javascript
var a = "a"console.log(isNaN(a)) //true 隐式转换为数值，然后判断是否是NaNconsole.log(Number.isNaN(a)) //false 不转换直接判断，只有数值型的NaN才是true，其他都是false
```

Object.is():与===比较 相似

```javascript
var a= 'a'console.log(Object.is(2,'2')) //falseconsloe.log(Object.is(Number(a),NaN)) //trueconsole.log(Object.is(a,NaN)) //false
```

