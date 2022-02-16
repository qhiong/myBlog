---
title: AJAX和Fetch和Axios
date: 2021-9-12
tags:
 - tag4
categories: 
 - JS-node
---

# AJAX

#### ajax介绍

```javascript
// 设置AJAX
var xhr=new XMLHttpRequest()
// 设置请求信息
// 第一个参数：请求方式
// 第二个参数：请求数据的网址，**也可以是配置文件**
// 第三个参数：async 表示是否异步，false表示同步；true表示异步
// 第四个参数：用户名和密码；可以用于传递数据
xhr.open("GET","网址",async,用户名，密码)
// 添加请求加载事件
xhr.addEventListener("load",loadHandler)
// 发送请求
// ArrayBuffer data  类型化数组
// Blob data  二进制大对象，是一个可以存储二进制文件的容器。
// Document data  文档对象
// DOMString? data  文本数据
// FormData data  数据对象，可以直接封装内容
xhr.send()
// 加载成功，得到响应结果
function loadHandler(){
    console.log(xhr.response)
}

// 请求头
注意： 必须写在open之后，send之前
xhr.setRequestHeader("Content-Type":"text/html;charset=utf-8")
也可以在里面添加：application/X-www-form-urlencoded
注意：在使用ajax的post向PHP服务器发送请求时，必须写这个请求头
在node部分，可以通过请求头传递数据AJAX；在服务器通过req.header获取

获取服务器的响应头，服务器必须允许客户端接收:Access-Control-Expose-Headers:"*":服务器允许客户端接受响应头
xhr.getResponseHeader
xhr.getAllResponseHeaders
//所有响应头和请求头自定义“X-”开头！！！！！！！！！！！！

//timeout事件：必须在open之后，send之前
一个请求在被自动终止前所消耗的时间
xhr.addEventListener("timeout",timeoutHandler)
xhr.timeout=时间
function timeoutHandler(e){
    xhr.abort() //触发改事件后主动关闭服务连接
}


xhr.readyState:当前通信的状态码
0：代理被创建，open()没被调用
1：open()方法被调用，url地址接收到了
2：send方法被调用完成，并且头部和状态已获得
3：下载中，服务器开始向客户端发送数据，接受过程
4：下载操作完成，服务器发送数据完全接收

xhr.status：服务器的状态
信息：100-101
成功：200-206
重定向：300-307
客户端错误：400-417
服务器错误：500-505
```

配置cors解决跨域问题：

1.Access-Control-Allow-Origin：源跨域

2.Access-Control-Allow-Methods：方法跨域

3.Access-Control-Allow-Headers：请求头跨域

AJAX三种发送数据方式

1.get

2.请求头和响应头（可以减少使用代理方式来发送数据）

3.post

#### 接口

路由：端口号后面携带的 http://localhost:4000/一级路由/二级路由/三级路由

同源策略：访问过去的必须时同一个策略

**GET/POST的不同之处：**

1.GET在浏览器回退时是无害的，而POST会再次提交请求。

2.GET产生的URL地址可以被Bookmark，而POST不可以。

3.GET请求会被浏览器主动cache，而POST不会，除非手动设置。

4.GET请求只能进行url编码，而POST支持多种编码方式。

5.GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。

6.GET请求在URL中传送的参数是有长度限制的，而POST么有。

7.对参数的数据类型，GET只接受ASCII字符，而POST没有限制。

8.GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。

9.GET参数通过URL传递，POST放在Request body中。

10.GET产生一个TCP数据包；POST产生两个TCP数据包,Firefox就只发送一次。

decodeURIComponent()将URI编码格式转换为汉字

encodeURIComponent()将汉字转为URI编码

**CommonJS只能用于node**

ES5前端：模块化开发用amd,cmd模块化

nodejs：模块化开发用commonJS

ES6：模块化开发：export 

#### 模块化区别：

**commonJS规范**

允许模块使用require方法来同步加载所依赖的其他模块，然后通过exports或module.exports导出需要暴露的接口。

**ADM规范**

AMD（Asynchronous Module Definition）异步模块定义，客户端规范。采用异步方式加载模块，模块加载不影响它后面语句的代执行。

在使用时，需引入require.js

**CMD规范**

CMD（Common Module Definition）通用模块定义，异步加载模块。

在使用时，需引入sea.js

**ES6模块**

ES6通过imort和export实现模块的输入与输出，import命令用于输入其他模块提供的功能，export命令用于规定模块对外的接口。

### Fetch

```javascript
var p=fetch("网址")====>得到的是promise的fulfilled的状态
async function getDataa(){
    var data=await fetch("网址",{method:"方法",body:数据,headers:{请求头}})
    data=await data.json()//解析json数据
    data=await data.text()//解析文本数据
}

fetch里面的是一个迭代器
```

#### 长连接和短连接

长连接：所谓长连接，指在一个TCP连接上可以连续发送多个数据包，在TCP连接保持期间，如果没有数据包发送，需要双方发检测包以维持此连接，一般需要自己做在线维持（不发生RST包和四次挥手）。

连接→数据传输→保持连接(心跳)→数据传输→保持连接(心跳)→……→关闭连接（一个TCP连接通道多个读写通信）； *
\*   这就要求长连接在没有数据通信时，定时发送数据包(心跳)，以维持连接状态；

短连接：短连接是指通信双方有数据交互时，就建立一个TCP连接，数据发送完成后，则断开此TCP连接（管理起来比较简单，存在的连接都是有用的连接，不需要额外的控制手段）；

连接→数据传输→关闭连接；

### Ajax和Axios和Fetch的区别

XMLHttpRequest对象的出现，JavaScript调用它就可以让浏览器异步地发http请求，然后这项异步技术就被称为Ajax。 之后jQuery封装了它，让异步结果更清晰的表现在一个对象的回调函数属性上。编写方式更简单，但出现了新的问题~回调地狱。 Promise为了解决异步编程的回调地狱问题诞生了。 随后有人把xhr对象用Promise封装了起来~它就是axios库(浏览器端)，axios在node.js环境是http模块的封装 后来又出现了一个可以异步地发http请求的api，就是fetch()。它并非是封装xhr对象的库。而是全新的JavaScript的接口。而且fetch api天生就是自带Promise的 现在的Ajax就有了两种方式: xhr对象和fetch()