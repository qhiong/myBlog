---
title: react介绍
date: 2021-8-19
tags:
 - tag4
categories: 
 - react-node
---

## react

> react  + react-dom 为什么分两个包？

因为react在设计之初就有跨平台的野望，所以react本身只专注vDom，具体到客户端的实现转换，有其他包来处理(react-dom for h5， react-native for native)。

## react-CDN-引入

为什么除了react/react-dom之外还要引入babel？

+ 为了解析jsx(html无法识别这种语法糖)

## 官方脚手架项目初始化

1. 初始化

```shell
npx create-react-app [project-name]
```

2. 配置项抽离

```shell
npm run eject
```

## jsx

1. 在react中，jsx是React.createElement的语法糖。

> createElement(type, props, children);

2. jsx内嵌入js表达式，只需要在js表达式外套一个花括号即可。

3. jsx的插槽可以嵌入数组，这意味着列表渲染直接嵌入数组就可以了。

4. jsx中给元素添加类名，不能用class(因为它与关键字class冲突)，要用className

### react中的事件

给vDom添加事件，只需添加onEventName即可。

```jsx
<div onClick={this.handleBoxClick}>+</div>
```

要注意的是，我们其实给vDom添加的是react自己封装的“合成事件”，它在映射到dom时，会被代理到挂载节点上。
(
    拓展: 17.0.1版本之前，是代理到document文档上。 17.s0.1后变动为root节点，即ReactDOM.render(App, rootEl)中的rootEl。
)


### 补充： es6-class

> class是构造函数的语法糖。

```js
class Demo {};
typeof Demo;
// 返回 "function"
```


### 