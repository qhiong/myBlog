---
title: react组件
date: 2021-8-23
tags:
 - tag4
categories: 
 - react-node
---


## 组件的本质即函数（类）

> react中，常规模式下，有两种类型组件。
> 注意点：

+ 组件必须以大驼峰形式命名，其他规范以小驼峰为准。
+ 严格的**单项数据流**！跟vue不一样，在react组件中，组件自身的props是只读的。

### 函数式组件

形如

```jsx
const Box = (props) => {
    return (
        <div>box</div>
    )
}
```

特点：

1. 就是函数啦，而且被标签化使用的时候,没有this；
2. 每次reRender，其实就是重新执行一遍这个函数。
3. 轻量。当函数式组件能满足我们的需求的时候，尽可能的使用函数式组件。

注意点：

1. 截止到16.8.0版本之前，函数式组件没有自身的状态(state)，也无法维护内部的值(每次reRender，代表这个函数被重新执行),因此我们通常会用它来写一些纯UI组件(只关注视图，数据从props中获取)。

2. 待续

### 类组件

形如

```jsx
class Box extends React.Component{
    render(){
        return (
            <div>box</div>
        )
    }
}
```

注意点：

1. 使用class来声明;
2. 继承自React.Component等react给提供的原型机(组件父类);
3. 必须具备render函数;
4. render函数必须要有返回值;

特点：

1. 就是写一个子类, 注意类组件里有this。
2. 每次reRender其实是执行了this.render这个函数。
3. 自带特殊的实例属性
   + props: 属性。
   + state: 状态，用this.setState去更新state时，组件视图会因此更新。原来是this.setState在更新状态后，会调用this.render。
4. 原型链上自带的特殊属性或方法
   + setState: 两种使用方式如下:
     + this.setState(assignState, callback); assignState是一个合并对象。注意，常规形势下，这是表现是异步的。所以第二个callback可以用来写入state更新后的操作。
     + thi.setState(setFn)
     + 常规下，在生命周期和合成事件中它的表现是异步的。如果外面套了一层计时器和延时器，它的表现就变成同步的了。


### 