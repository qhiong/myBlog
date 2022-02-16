---
title: DOM
date: 2021-8-16
tags:
 - tag4
categories: 
 - JS-node
---

# DOM

#### 基础知识

子节点：document.body.childNodes 列表心态

nodeName:节点名称（#text #comment #document 标签就是大写的标签名

nodeType:节点类型 ：元素1 属性2 文本3 注释8 文档9

nodeValue：节点值 (文本节点：文本 注释内容 元素节点不可用)

getElementsByTagName()和getElementsByClassName()获取到的结果是一个HTMLCollection，有三个方法：

length

item（index）===元素（index）

namedItem(name) 根据元素的name值

**注意：**没有forEach()方法

可以通过父元素获取后代中是否有这个标签的列表：

var divs=div.getElementsByTagName("div")

表单中：

getElementsByName() 根据标签中的name属性来获取，不能根据父元素获取后代中的name属性（id同）获取到NodeList

NodeList有以下几种方法：

.forEach(function(item,index,arr){})

.item(索引)

.keys()

.values()

.entries()

document.querySelector()和document.querySelectorAll()：根据选择器获取元素（兼容性不好）第二个获取是是NodeList;可以根据父元素获取

#### 节点遍历

body所有元素：document.body.children() 只获取子标签

body所有子节点：document.body.childNodes() 获取标签，文本，注释，换行等

.parentElement 父元素（HTML没有父元素）

.parentNode 父节点 （HTML的父节点是document）

.firstElementChild 第一个子元素

.lastElementChild 最后一个子元素

.firstChild 第一个子节点

.lastChild 最后一个子节点

.nextElementSibling 下一个兄弟节点

.previousElementSibling 上一个兄弟节点

.nextSibling 下一个兄弟节点

.previousSibling 上一个兄弟节点

#### DOM的创建

document.createChild(标签名)：根据标签名创建元素

父元素.appendChild(子元素)：将元素追加到父元素尾部

document.createDocumentFlagment() 碎片容器，用于已经拥有父容器里面要放入大量元素时

 **注意：**使用innerHTML +=时，会让页面重新加载，之前的标签不会被销毁，就会重新加载之前的标签，页面中之前的标签改变时，当前标签不会改变，所以以后尽量减少使用innerHTML 来加载页面 或者插入新元素

innerText只能获取当前元素的文本和后代文本，不保留空格和换行

父元素.insertBefore(新元素，要插入这个元素之前)  在某个元素之前插入

创建文本节点：

document.createTextNode(文本)

创建img :document.createElement("img")===new Image()

复制节点：

元素.cloneNode(false) 浅复制，只复制标签

元素.cloneNode(true) 深复制，会将这个标签内的元素及后代都复制

删除节点：

1.父删子：负元素.removeChild(子元素)

2.自己删除自己：子元素.remove()

替换节点：

父元素.replaceChild(新元素，被替换的元素)

插入文本内容：

元素.textContent(文本) //会保留元素后代中的所有节点，包括换行，只会渲染成字符串，不会解析html代码

#### DOM属性

创建dom元素没有加到页面之前，是放在内存的堆中

标签属性：给元素添加的标签属性

dom如何添加对象属性，获取对象属性

元素.setAttribute("key","值") 添加标签属性

元素.getAttribute("key") 获取标签属性

**注意：**设置标签属性的值必须是字符串，如果不是字符串会隐式转换为字符串，标签属性起名有规范：通常起名使用驼峰式，但是标签属性使用“-”连接；标签不区分大小写，css选择器不区分大小写；标签属性也是用“-”方式书写+

元素.removeAttribute("key") 删除标签属性

**标签属性的作用**：为了给标签作标记，并且快速有效的找到对应的标签

有些标签属性和对象属性公用的，通常来说，标签的系统自带的标签属性是共通的，除了class之外

任何标签都是HTML超文本，在页面创建时，会将超文本转换为DOM树，DOM树就是一个对象结构的树，对象属性就是直接作用于DOM树的对象结果，标签属性是作用于超文本内容，当设置了标签属性后，这个属性将会通过设置DOM而引起DOM对象属性的改变，并且确认是否进行回流和重绘。

input. abc=0 // 不会引起重绘和回流

input.setAttribute("abc","0") // 会引起重绘和回流（在页面添加之后）

**BOM对象属性设置不一定会引起重绘和回流，而设置标签属性，一定会引起重绘和回流。**

标签的属性名如果和属性值相同，我们通常可以在标签中设置为单独标签属性就可以了。

这种属性名和属性值相同的标签属性，在对象属性中使用布尔处理

属性名.checked=true

**注意：**div.setAttribute("class",'divs')

​           div.className="div1"

**总结：**HTML超文本----> DOM对象---->DOM对象渲染树

修改标签属性就是修改HTML超文本（标签），会引起DOM对象属性的改变。

修改DOM对象属性和修改DOM对象时，不一定会引起HTML超文本改变（只有部分系统标签属性会改变）

**哪些对象属性不会引起标签属性的改变：**

1.自定义对象属性

2.标签的属性名如果和属性值相同，不一定会改变（disabled可能会；checked会）

**如果设置了标签属性和设置了对象属性产生冲突时，遵循对象属性。**

div.style在变为DOM渲染树以后就会变为对象，CSSStyleDeclaration类型，因为对象属性名的要求不能使用“-”，所以所有css样式都将“-”去掉，使用驼峰式命名法。

当设置了style属性时，会自动更新转换为行内样式

div.style.width="50px"

超文本标记在页面运行到最下面时就会完成DOM树，并且完成DOM树的渲染。

标签中设置了行内属性和div.style.属性，通过div.style这种方式是可以获取到的，但是style样式中设置的是不能获取到的

如果要获取到标签的属性或者css样式设置属性，这些属性都是在DOM树渲染完成后计算得到的，因此无法获取到。

但是**DOM提供了一个临时可以进行计算的方法**：

getComputedStyle(div) 获取到div计算后的实际宽度

getComputedStyle(div,":after/:before") 获取计算后的样式，**只有after和before两种可以**

对于IE8及以下不支持

div.currentStyle 获取IE8及以下浏览器支持，火狐谷歌IE9以上不支持

**DOM设置样式都是针对某一个DOM元素的，这种设置时都会被设为行内样式**

##### 获取css样式

document.styleSheets 获取到列表

这个列表中放入到这里为止之前所有的style 设置css和link引入css列表内容，这个style是一个对象型列表，包括对象属性和索引下标

索引下标是指设置的样式属性

而属性是指所有样式属性

可以根据所有下标找到已经设置的属性名，然后根据属性获取到对应的属性值

**修改style样式**

```javascript
for(var i=0;i<document.styleSheets[0].cssRules[0].style.length;i++){
	var key=document.styleSheets[0].cssRules[0].style[i]
    // 因为css设置时不识别大小写，所以只能用-，不能用驼峰
    if(key==="background-color"){
        document.styleSheets[0].cssRules[0].style[key]="green"
    }
}
```

document.styleSheets style列表 不同style标签或者link，就会形成不同列表

document.styleSheets[0].cssRules 第0位style列表中，所有css设置列表

document.styleSheets[0].cssRules[0].tyle 第0位style列表中，第0个css列表中，所有设置样式

**添加style样式**

```javascript
var style =document.createElement("style")
document.head.appendChild(styles)
var styleSheet=document.styleSheets[document.styleSheets.length-1]
//styleSheet.addRule(选择器，样式，索引)
styleSheet.addRule(".div","color:red;",styleSheet.cssRules.length)
// styleSheet.insertRule(选择器{}，索引) 支持IE8及以下
styleSheet.insertRule(".div{color:red;}",styleSheet.cssRules.length)
// styleSheet.replace(要替换的内容，索引)
//styleSheet.removeRule(索引)
```

##### DOM部分属性

document.documentElement ==》HTML标签

document.body ==》body标签

clientWidth:客户宽度=宽度+padding-滚动条宽度（在不同浏览器和系统下不一样）

clientHeight:客户高度=高度+padding-滚动条高度（在不同浏览器和系统下不一样）

offsetWidth:偏移宽度=宽度+padding+border

offsetHeight:偏移高度=高度+padding+border

scrollWidth:滚动条宽度=容器内实际内容宽度+padding（左边的padding）

scrollHeight:滚动条宽度=容器内实际内容高度+padding

###### 元素

body和HTML

**body**

document.body.clientWidth就是body的宽度（浏览器宽度-滚动条宽度-2*margin大小）

document.body.clientHeight就是内容撑开的高度，最小是0

**html**

document.documentElement.clientWidth:html宽度：浏览器宽度-滚动条宽度

document.documentElement.clientHeight:html高度：浏览器可视高度

**body**

document.body.offsetWidth和document.offsetHeight

和document.body.clientWidth和document.body.clientHeight相同

**html**

document.documentElement.offsetWidth和document.documentElement.offsetHeight是实际html的内容宽高

**body和html的scrollWidth,scrollHeight**

body的scrollWidth和scrollHeight是body实际内容宽高

html的scrollWidth和scrollHeight是实际内容宽高,但是如果实际内容宽高小于视口高度时，scrollHeight等同于视口宽度

**总结**

1.任何没有放在页面中的元素，都无法获取它宽高和后面的位置，

2.不管获取宽高还是获取位置，都需要重新将渲染树拆开，并且重新计算css样式后才可以获取到，这就意味着使用获取宽高和位置会产生回流和重绘，如果只是获取，只会重绘；如果是设置，则会回流

###### 位置

clientLeft:左边线粗细

clientTop:上边线粗细

offsetLeft:相对于容器左上顶点坐标（父容器做定位），如果父元素没有定位，则向上寻找定位，直到html

offsetTop:

scrollLeft:滚动条左距离（可读可写）

scrollTop:滚动条上距离（可读可写）

滚动条高度：clientHeight/scrollHeight*clientHeight

滚动小条高度：clientHeight/scrollHeight*scrollTop

**body和html位置：**

低火狐谷歌版本中，窗口的滚动条是body的scrollTop,scrollLeft

但在现在的版本中，窗口的滚动条是html的scrollTop,scrollLeft


