---
title: react性能优化
date: 2021-11-18
tags:
 - tag4
categories: 
 - react-node
---


##  react**框架的性能优化之旅**。

> 性能优化是没有极限的。react在这条路上走了很久，做了很多尝试。

- 减少不必要的state
- 纯UI组件尽可能的使用函数式组件
- shouldComponentUpdate
- PureComponent
- renderProps
- hooks 可以让函数组件中使用状态和生命周期钩子用函数组件替代类组件，减少运行时间从而实现优化，useMemo使用缓存，减少固定UI的重复渲染，提高性能

### shouldComponentUpdate

在这个钩子里，我们可以手动地对比更新前后的props和state，来决定是否进行reRender，从而减少不必要的reRender。 也就是说，这个钩子可以做性能优化。

### PureComponent

事实上，多数情况下，shouldComponentUpdate没有使用的必要。react给我们提供了PureComponent这个原型机(父类)，它默认在shouldComponentUpdate中做了浅比较。 如果浅比较不通过，才会reRennder，反之如果浅比较通过，就不会reRender。 由于它的学习成本较高，使用者一时不慎可能会引发bug，因此它也很少被使用。