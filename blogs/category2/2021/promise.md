---
title: promise
date: 2021-8-17
tags:
 - tag4
categories: 
 - JS-node
---

# Promise

new Promise(function(resolve,reject){

​		resolve()   //只能传递一个参数

}).then(function(){

}).catch(function{

})

状态机三种：pending，fulfilled，rejected；默认是pending

​		当执行resolve函数时，状态被修改为fulfilled状态，这时候，如果再执行reject函数，判断当前状态是否是pending，如果不是pending状态就不再执行reject函数。

​		如果当前状态是pending状态，执行了reject函数时，状态被修改为rejected状态，再次执行resolve方法，发现状态不是pending状态，就会跳出不再执行resolve函数。

​		在Promise中，只能执行一次resolve或者一次reject

不管开始执行的是哪一种方式，执行后都会返回一个新的状态为fulfilled状态的Promise默认没有返回值时。

连续catch不被触发，连续then会被连续触发

##### 静态方法：

Promise.all()：将Promise对象的数组按照顺序从前向后全部执行完成，然后将每一次resolve传出的结果放在一个新数组中，并且将其在then中的函数中返回。

Promise.race()：查看谁的异步先完成就先返回谁。

Promise.resolve()：等同于：new Promise(function(resolve,reject){resolve()})

Promise.reject()：等同于：new Promise(function(resolve,reject){reject()})

#### async和await

阻塞式同步

async函数执行后将返回一个Promise对象

async function fn(){return 1}

fn.then((res)=>{console.log(res)}) //1

await必须写在async函数里面

await等待调用resolve（）之后再往下执行。

await只等待promise中的resolve函数执行，其他不会等待。