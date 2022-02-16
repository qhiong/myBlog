---
title: Flux架构思想
date: 2021-10-17
tags:
 - tag4
categories: 
 - react-node
---


### Flux

Flux 是一种 架构思想，简单来讲 就是: 状态提升到全局Store + Store内容分发给组件 + 组件交互updateStore然后更新组件。 就是这样一种 通过全局store同一管理数据(从而实现组件间数据共享)的架构思想。

redux与react-redux
基于这种思想，社区里已有各种各样成型的解决方案，其中，redux是通用性比较强的方案(兼容原生和绝大部分框架); 但它的使用较为麻烦，在react项目里，一般用 redux + react-redux + 配置中间件(根据项目需要配置) 这样的方式。 比如 dva = redux + react-redux + redux-saga + router （耦合了router也是dva的诟病所在）; 在hooks出现之后，react提供了 useContext这样的钩子，实现了redux的功能。 react-redux 的核心：Provider 与 connect

Provider和connect的底层原理
Provider容器组件底层: 把store打入 contextconnect; 高阶组件底层： 从context拿到store，然后打入到参数组件的props;

什么是高阶组件？ 高阶组件：接受一个组件为参数，return 出一个新的组件； 高阶函数：就是一个函数，接受一个函数为参数。
redux的核心：
createStore 与 disPatchcreateStore： 创建store
disPatch： 更新store的方法disPatch的规范/更新store的流程
react-redux流程
状态提升到全局与分发
createStore创建全局状态仓库
Provider和connnect进行状态的分发
状态更新
disPatch 一个 action （action就是一个对象，形如{type:'xxx',...prarams}）,基于action.type,触发对应的reducer（reducer是具体更新store的方法，纯函数）逻辑，从而更新store;