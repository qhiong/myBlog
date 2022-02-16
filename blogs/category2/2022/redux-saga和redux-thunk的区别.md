---
title: redux-saga和redux-thunk的区别
date: 2021-10-28
tags:
 - tag4
categories: 
 - react-node
---


### redux-saga和redux-thunk的区别

- 底层
  - 【redux-saga】是基于generater；
  - 【redux-thunk】是基于Promise

- 异步操作
  - 【redux-thunk】仅支持原始对象【(plain object)】，处理有副作用的action；
  - 【redux-saga】中处理了所有的异步操作, 异步接口部分一目了然。

- 优缺点
  - 【redux-saga】
    - 优点
      - 集中处理了所有的异步操作, 异步接口部分一目了然
      - action 是普通对象, 这跟 redux 同步的 action 一模一样
      - 通过 Effect, 方便异步接口的测试
      - 通过 worker 和 watcher 可以实现非阻塞异步调用, 并且同时可以实现非阻塞调用下的事件监听
      - 异步操作的流程是可以控制的, 可以随时取消相应的异步操作.
    - 缺点
      - 太复杂, 学习成本较高
  - 【redux-chunk】
    - 优点
      - 代码简洁
    - 缺点
      - 仅仅做了执行这个函数，不管其他操作，也就是说 thunk 使得 redux 可以接受函数作为 action, 
      - 从这个具有副作用的 action 中, 我们可以看出, 函数内部极为复杂. 如果需要为每一个异步操作都如此定义一个 action, 显然 action 不易维护.
        - action 的形式不统一
        - 就是异步操作太为分散, 分散在了各个 action 中



### redux-saga的使用流程

创建中间件：

```javascript
import createMiddleWare from "redux-saga"
// 创建一个中间件实例
const sagaMiddleWare = createMiddleWare()
```

将中间件打入仓库中

```javascript
// 创建一个仓库，打入这个中间件
const store = createStore(reduces,applyMiddleware(sagaMiddleWare))
```

启动这个中间件

```javascript
// 启动这个中间件
sagaMiddleWare.run(studentSagaList)
```

然后创建一个effect.js

```javascript
// 导入redux-saga/effect里面的put,call,takeEvery
// put({type:"",data:{}})
    // 传入一个参数，类似于redux里面dispatch传的参数{type:"",data:{}},会被reducer监听到
    put,
    // takeEvery(type,function)
    // takeEvery监听到type的动作，就会执行回调函数，除此之外，takeEvery可以同时监听到多个相同的action。
    takeEvery,
    // 调用call方法，执行异步请求
    call

// 对异步请求进行处理
function* fetchStudentList(actions) {
   // 执行异步请求 
    const results = yield call(getStuList, actions.filterObj)
    // 传入参数action
    yield put({
        type:"xxxxxxxxx",
        data:results
    })
}
// 然后创建一个Generator函数
// 注意：不能重名
function* studentSagaList() {
    yield takeEvery("xxxx", fetchStudentList)
}
```

<img src="C:\Users\yyh\AppData\Roaming\Typora\typora-user-images\image-20220112223624205.png" alt="image-20220112223624205" style="zoom: 50%;" />

PDA:指的就是是否用react native搭建过安卓应用，IOS应用

性能：

- 快
- H5只能使用浏览器支持的文件，安卓可以自己定义功能去使用（保存文件，相机，虚拟定位，设置手机桌面，信息通知，获取手机通讯录，）

react-native设置样式：

```javascript
import {StyleSheet} from "react-native"
const style =  StyleSheet.create({样式})
在render里面{style.样式名}
```

注意：在typescript里，const会被解析成var，不会有变量提升

### 