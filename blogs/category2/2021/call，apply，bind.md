---
title: 使用原生异或实现简单加密
date: 2021-4-20
tags:
 - tag4
categories: 
 - JS-node
---

### call、apply、bind

function fn(){}

fn()和fn.call()和fn.apply()一样：作用就是替换函数中的this指向

call()和apply()是用于执行函数的

如果带入第一个参数，在函数中的this将指向这个参数

```javascript
var o={a:1,b:3}
function fn(){
	console.log(this)
}
fn.call(o) //this指向o
fn.apply(o) //this指向o
```

如果第一个参数传入的参数是undefined和null时，在非严格模式时，this指向window，严格模式中，传入的是什么this就指向什么

##### call和apply的区别

指向函数时，传入原函数的参数方式不同

call从第二个参数开始传入参数，一个一个传入

apply从第二个参数传入，以数组的形式传入（也可以是列表），将数组中的数据作为函数的参数

##### bind:回调函数中改变this指向

绑定后返回新函数，执行这个新函数后，里面的this都是指向绑定的元素

```javascript
function fn(a,b){
    console.log(this,a,b) //{a:1,b:2} 2 3
}
fn.bind({a:1,b:2})(2,3)
```

### 