---
title: JS的this问题
date: 2021-5-12
tags:
 - tag4
categories: 
 - JS-node
---

# this指向

1. 任何情况下，直接在script标签中写入的都是window

2. 函数中的this，非严格模式指向window，严格模式指向undefined

3. 回调函数的this：setTimeout()和setInterval(),不管是否是严格模式，都会指向window，通过别的普通函数内执行当前回调函数中的this与2相同

4. 对象中的this：对象属性的this，执行该方法的是谁，this就指向谁；对象中箭头函数的this指向箭头函数外的上下文环境中的this

5. 箭头函数：不管是否是严格模式，this都指向箭头函数外上下文环境中的this

6. 默认状态下，数组部分遍历方法中回调函数中的this与2相同，**但是**，在所有数组的部分遍历方法中，如果是在最后一个参数中给入内容，那么这个函数中this将会被指向这个给入的内容（有thisArg的方法）

   ```javascript
   arr.forEach(function(){
       console.log(this) //{a:1}
   },{a:1})
   // filter forEach every some find findIndex map
   ```

7. 递归函数中的this与2相同

```javascript
function fn(){
    requestAnimationFrame(fn)
    console.log(this) //严格模式=>undefined 非严格模式=>window
}
```

8. 回调函数中，如果使用arguments对应项执行回调函数时，那么在被执行的函数中this指向回调该函数的那个上下文环境中的arguments

```javascript
function fn(){
    console.log(this)  //arguments
}
function fn1(f){
    arguments[0]()
}
fn1(fn)
```

9. 事件中的回调函数：this指向事件侦听的对象e.currentTarget

10. call,apply,bind方法执行时，this指向的是传入的第一个参数；如果传入的第一个参数是undefined或null时，非严格模式下指向window，严格模式下，传入的是什么就指向什么

11. 在类中：

    ES6类中：构造函数中的this指向实例化当前类所产生的新的实例对象，类中实例化方法中this指向：谁执行了该方法，this就指向谁；类中的静态方法，this指向该类或该类的构造函数；类中的实例化箭头方法，this仍然指向当前类实例化的实力对象

    ES5的原型对象中的this指向：在原型方法中，this指向实例化当前构造函数实例化对象（谁执行该方法，this就指向谁）

    ```javascript
    function Box(){}
    Box.prototype.play=function(){
        concole.log(this)  //谁调用就指向谁
    }
    Box.prototype.run=()=>{
        console.log(this) //类似于箭头函数  undefined或window
    }
    ```

    

