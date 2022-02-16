---
title: proxy
date: 2021-4-22
tags:
 - tag4
categories: 
 - JS-node
---

### 代理

```javascript
var obj={}
var p=new Proxy(obj,{
	get:function(o,key){
        return o[key]
    },
    set:function(o,key,value){
        o[key]=value
    }
})

// obj就是源对象，p就是代理对象
// obj有什么，p就有什么
// p里面有什么，obj不一定有什么
p.a=10 //这里调用了代理的set方法
obj.a  //这里不会调用代理的set方法
```

##### 代理的方法

```javascript
1.get
2.set
3.deleteProperty:function(o,key){
    return true
}
4.enumerable:function(o){}
5.getPrototypeOf:function(o){
    return Object.getPrototypeOf(o)
    return Reflect.getPrototypeOf(o)
}
6.setPrototypeOf:function(o,protoValue){
    Object.setPrototypeOf(o,protoValue)
    Reflect.setPrototypeOf(o,protoValue)
    return true
}
7.isExtensible:function(obj){
    return Object.isExtensible(obj)
    return Reflect.isExtensible(obj)
}
8.preventExtensions:function(obj){
    Object.preventExtensions(obj)
    Refelct.preventExtensions(obj)
    return true
}
9.getOwnPropertyDescriptor(target,属性名key){
    // 如果要修改desc,只能修改value
    return Object.getOwnPropertyDescriptor(target,key)
}
10.defineProperty(obj,key,desc){
    Object.defineProperty(o,key,desc) // 可以不写直接返回
    Reflect.defineProperty(o,key,desc) 
    return true  //设置属性的时候也可以直接使用这个方法
}
11.has(target,key){
    if(key==="__proto__") return false
    return key in target
}
12.ownKeys(obj){
    return Object.getOwnPropertyNames(obj)||Object.getOwnPropertySymbols(obj)
    return Reflect.ownKeys(obj) //只针对代理中拦截器使用 //可以获取所有属性，包括可枚举，不可枚举和Symbol
}
13.apply/////////////////重点  
function fn(a,b){
    console.log(a,b)
}
var p=new Proxy(fn,{
    apply(f,thisArg,argArray){
        return f.apply(thisArg,argArray)
    }
})
// p.call()和p()也可以直接执行调用apply
14.construct
class Box{
    a
    constructor(a){
        this.a=a
    }
}
var p=new Proxy(Box,{
    construct(F,argArr,newTarget){ // newTarget指的是代理对象p
        return new F(...argArr)
    }
})
```

### get,set

对象属性：1.通过等号赋值 2.存储数据

对象方法：1.执行可以传递多个参数  2.执行可以返回结果  3.执行可以完成多条语句运行

**set方法**：其中有且只有一个参数

**get方法**：不能有参数，而且必须使用return返回结果

```javascript
var obj={
    _c=0
    set c(value){
        this._c=10
    }
	get c(){
        return this._c
    }
}

obj.c=10说明执行了obj中的set方法，10就被赋值给了value。
obj.c直接执行，说明是执行get方法。
```

 对已有的对象添加set和get方法

```javascript
Object.defineProperty(target,属性,{
	enumerable:true,
    configurable:true,
    get(value){}
    set(){}
})
```

要求：

1.必须有一个临时变量来存储set赋值的结果，临时变量必须不可枚举和不可删除

2.成对出现set和get，如果只有一个set,这就意味着这个属性是只写属性，如果只有一个get说明是一个只读属性

### 
### 