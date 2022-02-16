---
title: JS运算符
date: 2021-5-8
tags:
 - tag4
categories: 
 - JS-node
---


    # 算数运算符

#### 1.算数运算符

​	**任何一个表达式都是具备返回结果的**

```javascript
var y = x = 4;
console.log(y,x) // 4,4+
// 先把x=4的结果赋值给y
// 然后再将 4 赋值给 x
```

##### 加法运算

​	任意类型和字符串进行相加时，会将任意类型的隐式转换为字符，然后首位相连

```javascript
var x = 1;
console.log(!x + 'aa') // falseaa
console.log({a:1;b:2} + 'aa' == {} + 'aa') //true
console.log([1,2,3] + 4) //1,2,3,4
console.log([1] + 4) //14
```

​			+ ！(非) 先隐式转换为布尔值，然后再取反

​	除了加法以外，任意类型 - * / %(取模) 都优先隐式转换为数值运算

```javascript
console.log('10'/null) //Infinity
console.log([10]/2) //5
console.log([]/2) //0
console.log(![10] / 2) //0
console.log(![]/2) //0
var x = 4;
console.log(x - (x + 5) + (x - "a")) //NaN
console.log(x - (x + 5) + '' + (x - "a")) //-5NaN
```

#### 2.赋值运算符和一元运算符

###### 	赋值运算符

```javascript
var a = 3;
a += 4;
//这个4就是步长，与+ - * / 运算符一致
var b = a += 1 + "a"
consloe.log(b,a) //41a 41a 
```

数值转换为字符串：a+=""；字符串转换为数值：b-=0

赋值运算符的优先级基本最低，除了，之外

###### 	一元运算符

一元运算符都会按照数值运算

```javascript
var x = "4"
consloe.log(x+=1) // 41
consloe.log(x++) //5
```

赋值运算符与一元运算符都是赋值处理，因此应该是变量运算。

```javascript
console.log(5++) // 报错：Uncaught SyntaxError: Invalid left-hand side expression in postfix operation
```

#### 3.关系运算符

关系运算符返回的是布尔值

在关系运算符中，会隐式转换为数值类型

NaN与任何数值比较时都是false

两个字符串比较时，会转换为Unicode编码进行比较

```javascript
console.log('a'>'b') //false
console.log(true > undefined) //false
console.log([]>-2) //true
console.log(![]>0) //false
console.log(![]<[]) //true
```

==：隐式转换两侧为相同类型后比较

===：不转换直接比较

```javascript
0 == false
0 == ""
"" == false
//这三个都会先隐式转换然后再进行比较
//undefined == null 但是不等于false 0 ""
// undefined == null 是用来判断变量是否有值
```

如果==比较时，两端的类型相同时，不隐式转换，直接比较

如果两端类型不同时，转换为对应的类型

```javascript
var y = 3;
var x = y > 3
console.log(x)
//这个是用来判断x是否是大于3的，如果大于则结果为true,否则为false,等同于
if(y > 3){
   x = true
}else{
   x = false
}
```

```javascript
// "" false 0  NaN undefined null
if(!x){

}

// null undefined
if(x==undefined){

}

// undefined
if(x===undefined){

}
```

#### 4.逻辑运算符

###### &&运算符

true && true => true (**返回最后一个的结果**)

true && false =>false

false && true =>false

false && false =>false（**当第一次遇到false的时候直接返回**）

返回结果：转换结果的值

```javascript
console.log(3 && 5) //5
console.log(0 && "") //0
```

```javascript
var x = 3
var y = x-3 && 6
console.log(y) //0
// 这个表示的是当x不等于3的时候，返回的就是后面的6，如果x等于3的时候，返回的就是0
// 这个类似于
if(x === 3){
   y = 0
}else{
   y = 6
}
```

###### ||运算符

true || true => true (**遇到true时直接返回**)

true || false =>true

false || true =>true

false || false =>false（**遇到false的时候继续向后查找，如果都没有，则返回最后一个结果**）

返回结果：转换结果的值

```javascript
var o;
o = o || "a"
consloe.log(o)
// 这个相当于是 如果o的值存在，则返回o的值，否则返回另一个值
// 等同于
if(!o){
	o="a"
}
// 这种思想通常用于单例模式中，有则继续使用，没有则初始化
```

###### ！运算符

#### 5.位运算符（30位以内，4个字节）

###### &运算符(凸显0的特征)

1 & 1 =>1

1 & 0 =>0

0 & 1 =>0

0 & 0 =>0

先转换为2进制，然后一位一位的进行&运算，运算结束后，再转换为10进制

###### |运算符（凸显1的特征）

1 | 1 =>1

1 | 0 =>1

0 | 1 =>1

0 | 0 =>0

先转换为2进制，然后一位一位的进行|运算，运算结束后，再转换为10进制

###### ^运算符

1 ^ 1 =>0

1 ^ 0 =>1

0 ^ 1 =>1

0 ^ 0 =>0

特点：

一个数X和另一个数Y的异或结果为Z,那么：

X^Y=Z

Y^Z=X

X^Z=Y

//根据这个特征，可以对密码进行加密

```javascript
String.fromCharCode(数字) //将Unicode编码转换为字符串
字符串.charCodeAt(索引) //将第几个字符串转换为Unicode编码
```

先转换为2进制，然后一位一位的进行^运算，运算结束后，再转换为10进制

###### ~运算符

~运算符：（位非运算符）：**加1取负**

```javascript
console.log(~5) //-6
console.log(~-8) //7
```

~运算符还可以用于对数字的取整,并且不会四舍五入·（过长的数据不可以用）

```javascript
console.log(~~4.5567) //4
```

###### 位移运算符

1.<<(先转换为2进制再进行移动补0)

```javascript
console.log(1<<8) //256=>2^8console.log(1<<4) //16 =>2^4
```

2.>>(先转换为2进制，然后再从右向左消)

```javascript
console.log(256>>6) //4// 100000000B 从右向左消6位 得到 100B 然后再转换为10进制
```

#### 6.条件运算符

variable = boolean_expression ? true_value : false_value;

```javascript
 var x = 3; x+=5 ? x+=3 : 4;//三元运算符的优先级比赋值运算符的优先级高，所以先计算5 ? x+=3 : 4 得到x=6 然后再将6值+=给x console.log(x); //9
```

#### 7.运算符的优先级

```javascript
(1)	. [] ()	字段访问、数组下标、函数调用以及表达式分组(2)	++ -- - ~ ! delete new typeof void	一元运算符、返回数据类型、对象创建、未定义值(3)	* / %	乘法、除法、取模(4)	+ - +	加法、减法、字符串连接(5)	<< >> >>>	移位(6)	< <= > >= instanceof	小于、小于等于、大于、大于等于、instanceof(7)	== != === !==	等于、不等于、严格相等、非严格相等(8)	&	按位与(9)	^	按位异或(10)  |	按位或(11)  &&	逻辑与(12)  ||	逻辑或(13)  ?: 	条件(三元)(14)  = oP =	赋值、运算赋值(15)  ,	多重求值
```


