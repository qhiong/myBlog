---
title: React Query
date: 2021-11-2
tags:
 - tag4
categories: 
 - react-node
---


### React Query

这是一个适用于 React Hooks 的请求库。 这个库将帮助你获取、同步、更新和缓存你的远程数据， 提供两个简单的 hooks，就能完成增删改查等操作React-Query 使用声明式管理服务端状态，可以使用零配置开箱即用地处理缓存，后台更新和陈旧数据。无需繁琐的配置，编写useReduce，以及维护全局状态，只要知道如何使用 Promise 或 async / await ，传递一个可解析数据（或引发错误）的函数，剩下的交给 React-Query 就好了，使用更少的代码获得更高的效率.



```javascript
 import { useQuery } from 'react-query'
 
 function App() {

   const {data, isLoading, isError} = useQuery('userData', () => axios.get('/api/user'));
   
   if (isLoading) {
     return <div>loading</div>;
   }
   
   return (
     <ul>
       {data.map(user => <li key={user.id}>{user.name}</li>)}
     </ul>
   )
 }

例子中 "userData" 字符串就是这个 query 独一无二的key。
可以看到，React-Query封装了完整的请求中间状态（isLoading、isError...）。
不仅如此，React-Query还为我们做了如下工作：

1.多个组件请求同一个query时只发出一个请求
2.缓存数据失效/更新策略（判断缓存合适失效，失效后自动请求数据）
3.对失效数据垃圾清理


```

**常用参数配置**

- staleTime 重新获取数据的时间间隔 默认0
- cacheTime 数据缓存时间 默认 1000 60 5 5分钟
- retry 失败重试次数 默认 3次
- refetchOnWindowFocus 窗口重新获得焦点时重新获取数据 默认 false
- refetchOnReconnect 网络重新链接
- refetchOnMount 实例重新挂载
- enabled 如果为“false”的化，“useQuery”不会触发，需要使用其返回的“refetch”来触发操作

**全局配置**

```javascript
import { ReactQueryConfigProvider, ReactQueryProviderConfig } from 'react-query';

const queryConfig: ReactQueryProviderConfig = {
  /**
   * refetchOnWindowFocus 窗口获得焦点时重新获取数据
   * staleTime 过多久重新获取服务端数据
   * cacheTime 数据缓存时间 默认是 5 * 60 * 1000 5分钟
   */
  queries: { 
    refetchOnWindowFocus: true,
    staleTime: 5 * 60 * 1000, 
    retry: 0
  },
};

ReactDOM.render(
    <ReactQueryConfigProvider config={queryConfig}>
        <App />
    </ReactQueryConfigProvider>
    document.getElementById('root')
  );
也可以单独配置，如下：

function Todos() {
   // 第三个参数即可传参了
   // "enabled"参数为false的化，不会自动发起请求，而是需要调用“refetch”来触发
   const {
     isIdle,
     isLoading,
     isError,
     data,
     error,
     refetch,
     isFetching,
   } = useQuery('todos', fetchTodoList, {
     enabled: false,
   })
 
   return (
     <>
       <button onClick={() => refetch()}>Fetch Todos</button>
 
       {isIdle ? (
         'Not ready...'
       ) : isLoading ? (
         <span>Loading...</span>
       ) : isError ? (
         <span>Error: {error.message}</span>
       ) : (
         <>
           <ul>
             {data.map(todo => (
               <li key={todo.id}>{todo.title}</li>
             ))}
           </ul>
           <div>{isFetching ? 'Fetching...' : null}</div>
         </>
       )}
     </>
   )
 }

```



