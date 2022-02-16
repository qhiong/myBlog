---
title: react函数式组件的hooks
date: 2021-9-30
tags:
 - tag4
categories: 
 - react-node
---


### react中的Hooks钩子

hooks式react在函数式组件中封装好的api,可以在函数式组件中使用；不能放在条件语句中使用

1.useRef (在函数式组件中使用，而createRef只能在类组件中使用)

- 保存函数式组件中的值，不会因为render而重置
- 也具备ref的能力（createRef）,标记DOM获取DOM实例，标记组件获取组件实例

2.useState

- const [state,setState] = useState(initValue)
  - 当initValue是简单类型时
  - 当initValue是对象时，setState会将初始值直接覆盖，不会进行assign合并

跟useRef一样，也可以使用多次

3.usecallback(fn, deps)

- **缓存的是函数本身**
- 当不传入deps时，使用useCallback相当于没有使用，当传入一个空数组时，会将里面的函数绑死。
- 当deps数组传入依赖项时，deps相当于一个监视器，当deps里面的数组值有改变时函数才会被重新更新。
- 尽量讲第二个参数写成[]，然后将依赖项放在回调的形参上，可以将性能最大化，但是调用的时候也还是会新创建函数，也是会消耗性能

4.useMemo（() => computeExpensiveValue(a, b), [a, b]）

- **缓存的是函数的返回值**

- 把“创建”函数和依赖项数组作为参数传入 `useMemo`，它仅会在某个依赖项改变时才重新计算 memoized 值。
- 传入 `useMemo` 的函数会在渲染期间执行。请不要在这个函数内部执行与渲染无关的操作，诸如副作用这类的操作属于 `useEffect` 的适用范畴，而不是 `useMemo`。
- 如果没有提供依赖项数组，`useMemo` 在每次渲染时都会计算新的值。

5.useEffect(副作用函数,[])

- 该 Hook 接收一个包含命令式、且可能有副作用代码的函数。默认在每一次render之后都会触发；无关渲染的业务逻辑叫做副作用
- 传入一个函数，每次在render之后都会去执行；会在ComponentDidUpdate和ComponentDidMount执行
- 也可以在这个函数里面返回一个函数，去清除副作用，会在每次添加副作用之前消除之前的副作用。在ComponentWillUpdate和ComponentWillUncount阶段消除
- 第二个参数是一个监听器，当监听器的数据发生改变之后才会重新执行，当监听器是一个[]时，就会锁死，相当于只是在ComponentDidMount执行了

6.useImperativeHandle(ref,createhandle,[deps])

- 必须和refs转发forwordRef一起使用
- 实质上就是在子组件里面使用ref.current = {}

```javascript
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput)
```

7.自定义hooks

另起一个js文件,使用use开头起名，然后将业务逻辑复制过去，导出，然后在需要的地方进行引用并解构

８.useLayoutEffect

与useEffect的使用一样，只是useLayoutEffect在每次渲染之前执行，一般用于提前的js动画渲染，而useEffect会在每次渲染之后执行的副作用

9.useReducer

**注意：**hooks的实现跟链表没有关系，但是hooks的存储是由链表的方式存储的，所以我们只能在顶层调用hooks，不能在循环和条件语句或嵌套函数中使用hooks