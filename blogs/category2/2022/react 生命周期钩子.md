---
title: react 生命周期钩子
date: 2021-9-7
tags:
 - tag4
categories: 
 - react-node
---

### react 生命周期钩子

> 不管是什么版本，都分三个阶段

1. 初始化阶段
2. 更新阶段(两种常态下引发更新的方式: this.setState ;   父组件更新;)
3. 卸载阶段


+ 16.0.0版本至今
16.3版本之前

只有类组件才有生命周期钩子

```javascript
constructor(props){} // 初始化配备this
componentWillMount(){}
render(){}
componentDidMount(){} // 一般用于挂载监听
```

更新阶段钩子

```javascript
componentWillReceiveProps(){} // 只有父组件更新才会引起子组件的更新,以此来触发这个钩子(一般不会触发)
```

```javascript
shouldComponentUpdate(){}//如果不给返回值或给fasle时，会阻断试图的更新，但是state的值会改变：这跟我们直接改变state的数据时是一样的。
componentWillUpdate(){}
render(){}
componentDidUpdate(){}
```

卸载阶段

```javascript
componentWillUnmount(){} // 通过if可以卸载组件
```

另外，外面还有一些特殊的声明周期钩子

```javascript
//比如处理错误边界的生命周期钩子
static getDerivedStateFromError() //渲染备用 UI 
componentDidCatch() // 打印错误信息
主要运用到捕获到错误不白屏，进行兜底处理
```

老版的react的开启context上下文的生命周期钩子

```javascript
getChildContext() //
```

16.3版本之后，由于fiber的出现，

```javascript
使用 componentWillMount, componentWillReceiveProps, and componentWillUpdate 这三个方法会收到警告。
```

```javascript
出现了几个新的生命周期钩子
static getDerivedStateFromProps(nextProps, prevState) // return出一个对象，和原来的state合并
// 这个函数会在每次re-rendering之前被调用
// 意味着即使你的props没有任何变化，而是父state发生了变化，导致子组件发生了re-render，这个生命周期函数依然会被调用
// 这个生命周期函数是为了替代componentWillReceiveProps存在的，所以在你需要使用componentWillReceiveProps的时候，就可以考虑使用getDerivedStateFromProps来进行替代了。
// 如果props传入的内容不需要影响到你的state，那么就需要返回一个null，这个返回值是必须的，所以尽量将其写到函数的末尾。
```

```javascript
getSnapshotBeforeUpdate(prevProps, prevState)的返回值作为componentDidUpdate的第三个参数使用
// 1：在render之前调用，state已更新
// 2：典型场景：获取render之前的dom状态
// 返回值传给componentDidUpdate， componentDidUpdate里面通过第三个参数接收到
```

![image-20220104154320343](C:\Users\yyh\AppData\Roaming\Typora\typora-user-images\image-20220104154320343.png)

