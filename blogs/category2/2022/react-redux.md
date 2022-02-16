---
title: react-redux
date: 2021-10-25
tags:
 - tag4
categories: 
 - react-node
---

# react-redux

### Redux是实现了FLUX思想的包

redux的核心： createStore 与 disPatch

createStore： 创建store

disPatch： 更新store的方法

react-redux结合了Redux和react的包

全家桶：react+react-redux+Redux

### 使用redux的流程

1.创建store====>createStore(reducer,初始化reducer的previousValue值)

2.通过Provider将创建的store打入context，将store数据分发下去，

3.通过connect高阶函数分发下去，先接收一个筛选函数mapStateToProps将需要的数据映射到props里面

4.通过this.props接收数据，然后需要视图交互了，就需要使用到dispatch（action）去修改，action是一个特殊对象，必须含有type这个属性

### disPatch的规范/更新store的流程

 disPatch 一个 action （action就是一个对象，形如{type:'xxx',...prarams}）,基于action.type,触发对应的reducer（reducer是具体更新store的方法，纯函数）逻辑，从而更新store;

![image.png](https://cdn.nlark.com/yuque/0/2020/png/205939/1608495359297-7ed29641-0793-4f74-8490-626ac7779413.png)

![image-20220110082109872](C:\Users\yyh\AppData\Roaming\Typora\typora-user-images\image-20220110082109872.png)


### 状态提升的好处

- UI和Model分离维护，代码更加结构化。
- 针对于容器组件，便于状态和业务逻辑的统一集成管理。
- 针对于子组件，保证UI组件的纯净。



#### redux-中间件

因为reducer是一个纯函数，不能执行异步，所以使用redux-saga去先拦截dispatch里面的内容 通过判断是否有异步等操作，有就先执行，然后再去执行reducer

redux-saga使用了ES6的Generator功能，让异步的流程更易于读取、写入和测试