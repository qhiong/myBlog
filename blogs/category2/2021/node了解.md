---
title: Node了解
date: 2021-10-2
tags:
 - tag4
categories: 
 - JS-node
---

# NODE

就是一个开发应用程序的API

**作用**

1.可以操作数据库

2.可以读取和写入当前服务器文件夹和文件

3.可以处理二进制流文件和数据

4.不能操作DOM和BOM，以及相关事件部分

#### 模块化开发

nodejs只有一个主入口文件，在文件入口需要调用需要其他js文件，这些文件就需要写成模块化。

nodejs的模块叫做commonJS    只适用于ES5的模块化

在nodejs中

导出：module.exports=.........

导入：require("./........")  不需要写扩展名；但是必须写**"./"**

如果没有./ 则nodejs会认为是系统的nodejs路径或者node_modules路径下

在nodejs中使用ES5和ES6的导入和到处时，需要在package.json中添加type:"module"：

导出：export default....

导入：import....... from.........

如果导出问价之后有重名，则需要采用   ：  来取别名

**注意**：在执行ES6模块化开发nodejs时，需要执行的时候在后面加上扩展名：node 名字.扩展名

在入口文件index.mjs中导入时也需要添加扩展名        import a from "./a.mjs"

#### nodejs连接服务器

```javascript
var http=require("http");// 超文本协议
// var https=require("https")// 需要安全权限
/**
 * createServer 创建一个服务
 * createServer 中参数是一个回调函数马，而回调函数中参数有两个，一个是request，一个是response
 * req的意思是请求，类型是：IncomingMessage  请求头
 * res的意思是响应，类型是：serverResponse   响应头
 * 消息分为两个部分：一个是消息头，消息体
 */
http.createServer(function(req,res){
    // setHeader一次只能设置一个头消息；必须只能写在writeHead前面
    // res.setHeader("Content-Type","text/html;charset=utf-8")
    // writeHead可以设置很多头消息，并且包含了状态码
    res.writeHead(200,{ //响应头消息
        "Content-Type":"text/html;charset=utf-8",
        // 允许跨域访问发送数据
        "Access-Control-Allow-Origin":"*",
        // 允许跨域时修改请求方式
        "Access-Control-Allow-Methods":"*",
        // 允许客户端发送来自自定义的请求头
        "Access-Control-Allow-Headers":"X-name",
        // 如果需要发送自定义响应头，需要浏览器可以获取必须使用这个来设置需要发送的自定义响应头
        "Access-Control-Expose-Headers":"X-Session-Id",
        // 响应头传递数据
        "X-Session-Id":"1011101"
    })
    // 写入响的消息
    res.write("hello")
    // 结束发送；要求end必须最后执行
    res.end()
    // 如果只有一条数据发送，可以直接写在end里面
    // res.end("你好")
}).listen(4800,"10.9.28.123",function(){
    // 创建的服务有一个listen方法，开启服务侦听，端口号设置
    // 后面需要有当前服务的域名//如果不写可以直接输入localhost也可以输入其他IP加上端口号进行访问
    // 函数是服务创建后自动执行的函数
    console.log("创建服务成功后执行！");
})

```

#### nodejs连接mysql

```javascript
1.下载MySQL模块
npm i mysql
2.引入MYSQL模块
var sql=require("mysql")
3.连接MySQL数据库
var db=sql.createConnection({
    url:"localhost",
    port:3306,
    user:"root",
    password:"root",
    database:"game"
});
4.判断连接是否成功
db.connect(function(err){
    if(err){
        console.log("连接失败")
        return
    }else{
        console.log("连接成功")
    }
});
```

