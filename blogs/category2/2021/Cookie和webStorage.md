---
title: Cookie和webStorage
date: 2021-7-17
tags:
 - tag4
categories: 
 - JS-node
---

# Cookie和webStorage

### 1.Cookie

  本地存储：存储在本地文件中，但是这个本地文件不可找到.。cookie存储的是字符串

document.cookie="name="值" "

cookie中只能存储字符串，如果是对象和数组，就需要使用JSON.stringify转换字符串存储。

##### cookie的特征：

1.cookie存储有时效性，当关闭浏览器时，就会自动消失。

2.通过浏览器设置去清除cookie

3.可以通过浏览器设置不保留cookie

4.在浏览器的控制面板中的存储项有cookie，可以选择清除或者全部清除。

```javascript
//获取所有cookie
function getCookieObj(){
    var obj={}
    document.cookie.replace(/([^;\s]+)=(.*?)((?=;)|$)/g,function(item,$1,$2){
        try{
            $2=JSON.parse($2)
        }catch(e){}
        obj[$1]=$2
    })
    return obj
}
```

cookie只能做临时存储，但如果有需要，外面也可以指定存储时间。

document.cookie=”key=value;expires=“+date.toUTCString()   **只能设置UTC时间**

如果设置当前时间的cookie，则就会被清除。

##### cookie最重要的特征：

1.可以在同一个域的客户端和服务器进行传递。当网页访问或跳转到服务端的程序中，**cookie会自动携带到服务器**。因为同域访问中都会获取到该域中存储的cookie。

2.cookie因为会自动携带在客户端和服务端中自动传输，cookie本身就不能太大，不超过5k

3.当关闭浏览器时，会话级的存储会被清除，有时间设定的数据会被保留。

4.cookie存储时，是按照域来存储不同域中的数据是不能互相访问的，而且cookie存储时也是根据目录结构存储，这样的目录结构分为顶级域，一级域，二级域等，cookie是按照各种域存储的，可以从低级域访问到高级域的存储数据，但是高级域不能访问到低级域。

www.baidu. com（顶级域）/news（一级域）/article(二级域)

还可以设置cookie的路径：document.cookie="key=value;path="'路径地址“'；

5.cookie是明文的，不安全，因此存储一些数据时，需要考虑加密

### WebStorage

分为：localStorage和sessionStorage

#### 1.localStorage

设置值：1.localStorage.setItem(key,value)

​				2.localStorage.名=值

获取值：1.localStorage.getItem(key)

​				2.localStorage.名

方法：

1.localStorage.clear()   清空

2.localStorage.getItem() 获取值

3.localStorage.length  长度

4.localStorage.key()  所有键

5.localStorage.removeItem() 删除

6.localStorage.setItem() 设置值

遍历localStorage所有的值：

Object.keys(localStorage).forEach(key=>{})

#### 2.sessionStorage

所有用法与localStorage一致

##### 区别

1.sessionStorage是会话级存储，localStorage是长期存储

2.sessionStorage与localStorage存储量大，可以达到5M左右，而cookie存储只有5K，webStorage不会自动在客户端和服务器传送。

3.sessionStorage区分窗口，同一个页面不同窗口打开也不共享；localStorage是按照域存储，不区分路径，cookie按域存储，区分路径

4.localStorage有storage事件驱动，可以完成跨页面处理内容

