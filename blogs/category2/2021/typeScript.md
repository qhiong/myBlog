---
title: typeScript
date: 2021-12-20
tags:
 - tag4
categories: 
 - JS-node
---

# TypeScript

### 基础类型

​	类型使用范围：

​		1.定义变量

小写类型都是栈中的变量，大写的类型就是栈中和堆中的类型

例如：n:number = 1 => n=new Number(1)  错误

​			m:number = 2 =>m=new Number(2) 正确

正常声明变量，声明时可以不用赋值：var n:number;n=10

​		2.函数返回值 

函数声明返回值，如果声明非void类型，就必须返回对应的类型

​	function fn():number{return 2 // 必须返回相应类型}

如果需要返回一个undefined，或者不返回内容可以设置 number|undefined 或 number|void

如果不返回值，使用void定义   function fn():void{}

参数?:类型  =>> 参数:类型|undefined=undefined

在类中定义属性时，这个属性的类型设定后，必须给初始值或者在constructor中给与初值 

```javascript
class Box{
	a:number;
	constructor(){
        this.a=1
    }
}
如果希望这个属性在后面赋值则可以设置：
属性：类型|undefined=undefined
属性?:类型
```

构造函数不能设置返回类型

在Set访问抽象类中设置属性可以不用赋初始值，也注意使用?:和这个内容的区别

​		3.函数的参数

​		4.接口和抽象类的声明

在接口被应用时没有?:的这个写法必须在类中初始赋值或构造函数中赋值，有?:的写法时可以不用初始赋值。

​		5.接口和抽象类的声明

### 类型变量

number , string , boolean , undefined , null , object(注意与null结合) , array , 元组 ， 枚举 , Any , void , never

声明对象时不能重新赋值和添加属性

##### 数组声明

一维：

var arr:number[]=[1,2,3]

var arr:Array<number>=[1,2,3]

二维：

var arr:number[] []=[[1,2],[3,4]]

var arr:Array<Array<number>>=[[1,2],[3,4]]

var arr:[number,string]=[1,"a"] // 不允许这样写，会影响运行效率

##### 元组声明

var arr:[number,string]=[1,"a"] 

给定几个类型，就给定几个值，一一对应类型

元素类型最好不要添加和删除

##### 枚举声明

一般用于消除魔术字符串

enum Color{RED,GREEN,BLUE}

无赋值时，返回的结果是下标  console.log(Color.RED) //0

有赋值时，给定赋值结果

枚举类型不能重新赋值，只读，或者称为常量

void声明：

function fn():void{}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

void类型流类型于undefined，用于函数没有返回值。

var a:void = undefined

##### never声明

永远不会向后执行

function fn():never{throw new Error("错误")}

##### 对象声明

var o:object={a:1,b:2}

var o1:object = Object.create(o)       正确

var o2:object = Object.assign({},o)   错误 因为不知道o的属性类型，不能复制，但在ES2015以后可用

var o3:object = {s:10}

o3 = {...o}  解构o  不会保留原有的o3属性

### Symbols

var a:symbol = Symbol()  // ES2015以后才能使用

在tsconfig.json中设置lib:["ES2015"]

### 断言

var a:number|string 

var s:number=(a as number)+1

### 接口

接口不能设置初始值

##### 对象使用接口

方法一：可扩展属性

```javascript
interface IBox{
	a:number;
    b:string;
    [key:string]:number|string;带任意数量的string类型 
}
```

方法二：当参数设定时，可以不写interface定义，直接使用这种接口写法规定其类型

```javascript
function fn(obj:{a:string,b:number})
或 function fn(obj:{[key:string]:string|number}){}
```

##### 可选属性

interface IBox{a?:number}

##### 只读属性

```javascript
interface IBox{
	readonly EVENT_ID="event_id";
    a:number;
}
var obj:IBox={Event_ID:"event_id",a:1}
obj.a=2
obj.EVENT_ID="ddd"   不能修改只读属性
```

在接口声明的所有属性，可以修改，但是readonly不能修改，只能在初始赋值时定义

在ES6中不能用const定义常量，可以使用get或Object.defineProperty

##### 函数定义接口

只能使用匿名函数定义函数

```
interface IFun{
	(a:number,b:string):void
}
var fn:IFun=function(a:number,b:string):void{}
```

##### 可索引的类型（数组使用接口）

```javascript
interface IArr{
    [index:number]:string  //只能写数据
}
var arr:IArr=["a","b","c"]


interface IReac{
    width:number;
    height:number;
}
interface IArr{
	[index:number]:IRect
    a:number
}
var arr:IArr={a:1} => 此时的arr是一个对象
arr[0]={width:30,height:30}
```

##### 类与接口

interface IBall{.......}

class Ball implements IBall{........}

##### 对于类型的接口型 归类

```javascript
interface A{update():void}
class B implements A(update():void){}
class C implements A(update():void){}
var arr:Array<A>
arr.push(B)//
arr.push(C)//因为BC都实现了A，所以可以添加在数组里面
```

##### 构造函数接口

```javascript
interface ID{new (n:number):IE}
interface IE{tick():void}
class D implements IE{
	constructor(a:number){}
	tick():void{}
}
class E implements IE{
	constructor(b:number){}
	tick():void{}
}
function fn(cla:ID,n:number):IE{
	return new cla(n)
}
var d=fn(D,3)  // D{}
var e=fn(E,4)  // E{}
```

##### 接口继承

一个接口可以继承多个接口，创建出多个接口的合成接口

let a=<A>{}  // 根据接口创建对象

#### 混合类型

```javascript
interface Counter{
    (start:number):number////函数接口
    reset():void
}
function getCounter():Counter{
    let counter = <Counter>function(){}
    counter.reset():void{}
}
```

#### 接口继承类

```
接口会将类上的方法和属性调用过来，在实现时都要将其实现
```

### 类

##### 修饰符

public：公有的：该类的实例化对象可以调用public定义的属性和方法（包括静态，只读），可以覆盖和重写public方法和属性

private：私有的：该类的实例化对象不可以调用private定义的属性和方法（包括静态，只读），子类的方法中不可以实例this调用获取private定义的属性和方法（包括静态，只读）

protected：受保护的：该类的实例化对象不可以调用protected定义的属性和方法（包括静态，只读），子类的方法中可以实例this调用获取protected定义的属性和方法（包括静态，只读），可以覆盖和重写protected方法和属性

**override**：重写，覆盖

超类或者父类中已经存在该方法，但这个方法是私有的，因此不能重写和覆盖.

##### 抽象类

​	不能直接实例化的类，用来继承，可以实现自己的属性和方法，是接口和类的混合体，一般作为基类来使用.

```javascript
abstract class A{
    abstract run():void;
}
class B extends A{
    public run():void{
        console.log("run")
    }
}
```

```javascript
let a:typeof A=A    =====>说明a是类A这个类型
类似于 let a = A 但是给了a一个类型
```

**文件.d.ts 可以有提示功能**

### 函数

```javascript
let myAdd:(x:number,y:number) => number =function(x:number,y:number):number{return x+y;}
等价于：
let myAdd:(x:number,y:number) => number
myAdd=function(x:number,y:number):number{
    return x+y
}
```

##### 剩余参数

```javascript
function max(...arg:Array<number>):number{return 1}
```

### 泛型

```javascript
function getValue<T>(n:T):T{
	return n
}
getValue<number>(5)
```

##### 接口泛型

```javascript
interface fns<T>{
    (x:T,y:T):T
}
function fn1<T>(x:T,y:T){
    return x+y
}
let fn:fns<number>=fn1
let s:number=fn<number>(3,5) ===> 8
```

##### 泛型类

```javascript
class A<T>{
	zeroValue:T;
	add:(x:T,y:T)=>T
}
let a=new A<number>()
a.add = function(x,y){return x+y}
```

##### 泛型约束

```javascript
intereface IArg{
    num:number
}
function fns<T extends IArg>(item:T):void{}
fns<IArg>({num:5})   正确
fns<number>(5)   错误
```

在泛型中使用类类型

```javascript
function create<T>(cls:{new():T}){  // 类传参，传的是类类型
	var a:T=new cls() //A这个
}
create<A>(A)
function createItem<T>(item:T){}
```

### 枚举

##### 外部枚举

外部枚举：declare 用来描述已存在的枚举类型的形状；可用在.d.ts中。

### 装饰器

