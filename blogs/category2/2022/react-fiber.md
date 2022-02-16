---
title: react-fiber
date: 2021-10-30
tags:
 - tag4
categories: 
 - react-node
---

### fiber

**起因**

当前版本的react的diff是同步的，一旦开始不可中断，如果vDOM树足够庞大，则渲染时间过长，页面就会有延迟，用户看见的页面就会有卡顿现象。

以前是以一个树为单位，不可中断；现在是以一个节点为单位，可以中断；

##### fiber节点

React16.3版本，在vDom结构的基础上，添加了链表节点的特性：还标记了一些不安全的钩子child,sibling,return(指回父节点),last(指向更新前的对象)

##### react并发模式 ---beta版本 ---fiber架构

预计划React17版本上，推迟到了react18版本

并发模式：将以树为单位改为节点为单位

requestIdleCallback()

先询问这个vNode是否有空闲，然后使用generater去暂停运行，

render的时候有可能会多次调用初始化钩子，rerender的时候可能会多次调用修改的钩子

不安全的钩子彻底弃用，启用新的钩子：static getDerivedStateFormProps,可以替代启用的时候的功能，也可以替代更新阶段的钩子；getSnapshotBeforeUpdate:在更新之前获取快照

<img src="C:\Users\yyh\AppData\Roaming\Typora\typora-user-images\image-20220113164336892.png" alt="image-20220113164336892" style="zoom: 50%;" />



