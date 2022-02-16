---
title: react-context
date: 2021-10-8
tags:
 - tag4
categories: 
 - react-node
---


### context

**16版本之前

```javascript
import React from 'react';
import PropTypes from 'prop-types';
import './App.css';

class Child extends React.Component{
  static contextTypes = {
    a: PropTypes.number
  }
  render(){
    console.log(this.context,'Child')
    return <div />
  }
} 

// props:  color : stirng    
export default class App extends React.Component{
  static childContextTypes= {
    a: PropTypes.number
  }
  getChildContext(){
    return {
      a:1
    }
  }
  render(){
    return (
      <div>
        <Child />
      </div>
    )
  }
}
```

**16版本之后**

console.log(React.createContext({}))

```java
默认有两个组件   
   Consumer
   Provider 
const context = React.createContext()
const { Provider,Consumer} = context
提供者(祖宗组件)：
// 将组件嵌入在提供者里面
<Provider value={{count:1}}>
    <Parent />
</Provider>    
消费者(孙子组件)：
<Consumer>
    //必须是嵌入一个函数
	{
        (value)=>{
            return <div>{value.count}</div>
        }
	}
</Consumer>
```

### 