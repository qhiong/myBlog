---
title: React.memo
date: 2021-11-18
tags:
 - tag4
categories: 
 - react-node
---

# React.memo

是一个高阶组件，作用与pureComoponent一样，都是用作性能优化，不同的是React.memo是用于包裹函数式组件，而pureComponents只能用于类组件；

React.memo(纯函数的组件，用于对比props控制是否刷新（是一个函数，与shouldComponentUpdate一样返回布尔值）)