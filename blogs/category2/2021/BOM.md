---
title: BOM
date: 2021-8-2
tags:
 - tag4
categories: 
 - JS-node
---

# BOM

定义：Browser Object Model 浏览器对象模型

Model：一种标准

Object：对象

#### window

```javascript
1.open(网址)打开页面
	参数1：网址
    参数2：网站标题
    参数3：网站宽高
2.close() 关闭
3.innerWidth 可视宽高
4.innerHeight 可视高度
5.outerWidth：窗口的宽度
6.outerHeight：窗口的高度
7.screenX 窗口的位置距离屏幕左上角位置
8.screenY 
9.screenLeft
10.screenRight
```

#### BOM组成

##### document

##### location

```javascript
1.reload() 
2.location.href="网址"
//区别就是一个是属性，一个是方法；相同点：有历史记录
3.location.assign(网址)
4.location.replace() //没有历史记录
5.location.hash() 锚点标记
// 当hash和search同时存在时，hash只能写在？后面
6.location.search() 当前网址路径
7.location.pathname 当前网址路径
8.location.hostname() 域名
9.location.port() 端口号
10.location.protocal() 协议
```

##### screen

```javascript
1.width 屏幕实际宽度
2.height 屏幕实际高度
3.availWidth 屏幕减去附件的宽度
4.availHeight 屏幕减去附件的高度
```

##### navigator

```javascript
1.userAgent 浏览器的基本信息
2.platform 运行的机器型号
3.geolocation.getCurrentPosition(function(pos){
    console.log(pos)
},function(err){
    console.log(err)
})//谷歌浏览器采用的是谷歌地图，谷歌地图不支持获取位置
```

##### history

```javascript
1.history.back() 回退
2.history.forward() 前进
3.history.go(数字) 0表示刷新页面，正数表示前进几步，负数表示后退几步
4.history.length 历史长度
5.history.pushState() 创建历史，并在历史中插入状态数据
6.history.replaceState() 替换当前历史记录的状态数据
7.history.state() 历史中当前的状态数据
```

#### 网页

CSR：Client Side Render 客户端渲染：没有历史记录

SSR：Server Side Render 服务器渲染：静态页面可以使用SEO优化，能被搜索引擎搜索到

SEO优化：搜索引擎优化：（title，<meta search="" keywords=""> img h1）







