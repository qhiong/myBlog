---
title: JQuery
date: 2021-11-19
tags:
 - tag4
categories: 
 - JS-node
---

#  99jQuery

主要功能：

•1.像CSS那样访问和操作DOM

•2.修改CSS控制页面外观

•3.简化JavaScript代码操作

•4.事件处理更加容易

• 5.各种动画效果使用方便

•6.让Ajax技术更加完美

•7.基于jQuery大量插件

•8.自行扩展功能插件

$:jQuery函数 ===>function $(){}===function jQuery(){}

console.log($===jQuery)  // true

连缀

$("div").text()//给每个div添加文本

jQuery对象不能使用js的方法，比如textContent，jQUery中将js所有方法重新转换为数组。

将jQuery对象转换为数组：Array.from($('div'))

将DOM对象转换为jQUery对象：$(DOM对象) 比如：$(div)

### 方法：

```javascript
$(".div .div1")=$(".div").find(".div1")
$(".div1").children() ==$(".div1>*")
$("#div1").next() == $("#div1+*")
$("#div1").nextAll()=== $("#div1~*")
$("#div1").nextUntil("#div2")  div1和div2之间的元素
$("#div1").prev() //上一个
$("#div1").prevAll() //上面所有元素
$("#div1").prevUntil("#div1") //div2向上到div1所有元素
$("#div1").siblings() //所有兄弟元素
```

### 属性选择器

```javascript
$("[id]")
$("[type=text]")
$("[type^=t]")
$("[type$=t]")
$("[type|=text]")
$("[type~=text]")
$("[type!=text]")
$("[type*=text]")
```

### 过滤器

```javascript
$("li:first")//last
$("li:first-child")//last
$("li:first-of-type")//last
$("li:nth-child(1)")
$("li:nth-of-type(1)")
$("li:nth-child(odd)")
$("li:nth-child(even)")
$("li:not(.li)")
$("li:even")
$("li:odd")
$("li:eq(2)") //选择jQUery对象列表中第二个jQuery对象
$(".li1:gt(2)") // li1元素列表中大于2下标的所有jQUery对象
$(".li1:lt(2)") // li1元素列表中小于2下标的所有jQUery对象
$(":header") //h1~h6所有内容
$(":animated") //所有动画的元素
$(":focus") //所有聚焦对象
```

方法比过滤器速度更快

### 方法

```javascript
$("li").eq(2) == $("li:eq(2)")
$("li").first() == $("li:first")
$("li").last() == $("li:last")
$("li").not() == $("li:not()")
$("li:empty") //空元素，空内容
$(":has(selector)") // 查看后代中是否拥有selector
$(".div1:parent") //判断div1是否是空元素
$("li:contains(1)") //判断后代内容是否含有1字符的li、
方法
$("div").has(".div1")
$("div").parent() //获取当前div的父元素
$("div").parents() //获取当前div的所有父元素列表
$("div").parentUntil("body") //获取所有元素列表中向上到body为止之间的所有父元素
$(":hidden") //不可见元素，不会获取visibility:hidden
$(":visible") //可见元素
$("li:only-child") //唯一一个子元素
$("li"):is(".li1") //判断li中是否有li1
$("li").hasClass("li1") //判断li中是否有li1  只能判断class
$("li").slice(开始，结束)
```

### jQuery遍历

```javascript
$.each(数组/对象，function((index,value)=>{}))

$("div").each(function(index,value)=>{})

$("div").text() //获取div所有的内容，返回所有div的文本内容组成字符串

$("div").text(function(index,value)=>{设置新的每一个div的内容})

$("div").html() ==>innerHTML  //仅能获取列表的第一个元素内容

$("div").html(function(index,item)=>{})

$("input").on("input",function(){

	$(this).value //输入文本内容时获取内容

})
```

### jQuery属性

```javascript
$("div") //attr  prop  data
1.attr  标签属性 ，获取第一个标签属性
$("div").attr("名字","值") //每一个都会添加
$("div").removeAttr("名字") //每一个都会删除
$("div").attr("a",function((index,value)=>{}))
$("div").attr({"名字","值","名字","值"}) 
$("div").attr({"名字",function(index,value){},"名字",function(index,value){}}) 
2.prop   对象属性 
$("div").prop("abc",10) //设置的是DOM属性值
这里直接设置在DOM属性上了，可以修改DOM对象属性值
$("div").removeProp("a")  //prop不能删除标签属性
3.data  数据属性
// 只设置数据值，不影响标签的显示和特征
$("div").data("ss",11)
设置在DOM对象的其中一个属性的映射对象中
$("div").removeData("ss")
```

### jQuery的css

**设置的是行内元素**

$("div").css("名"，"值")

$("div").css("名") //直接可以获取到DOM的计算后的css样式，不用用js中的getComputedStyle()

$("div").css({width:50,height:"40px"})

$("div").css(["width","height]) //获取第一个元素的多个css

$("div").addClass("class")

$("div").removeClass("class")

点击切换

$("div").toggleClass("class") //切换样式

属性样式：

$("div").width()//可以获取到css以及行内样式计算后的宽度，而且是数值

$("div").height()

$("div").innerWidth() //获取内容宽度和padding宽度，设置时，会自动减去padding

$("div").outerWidth() //获取内容宽度和padding宽度和border，设置时，会自动减去padding和border

$("div").outerWidth(true) //获取内容+padding+margin+border，不能设置

定位：

$("div").offset() //  相对于page页面左上角，可以修改

$("div").position() //相对于父容器  不能修改

$("div").offset({left:600,top:600}) //设置绝对于页面左上角位置

$("div").scrollLeft()

$("div").scrollTop()

### DOM

创建DOM元素：

```javascript
$("<div></div>")
$("body").append("<div></div>") 向body添加元素，返回body
$("<div></div>").appendTo("body") 向body添加元素，返回div
$("p").prepend("<div></div>")  向p前面添加div 返回p
$("<div></div>").prependTo("p")  在p前面添加div 返回div
$("div").after("<p></p>")  p插在div后面，成为div的下一个兄弟元素
$("<p></p>").insertAfter("div")  p插在div后面
$("div").before("<p></p>") 向div前面添加p元素
$("<p></p>").insertBefore("div")  将p插在div前面
$("span").warp("<div></div>")  包裹
$("span").unwarp()  去掉包裹
$("span").warpAll("<div></div>")
$("span").warpInner("<p></p>")
```

复制

```javascript
$("p").clone(false).appendTo("body")  //clone都是深复制，false不复制事件，true复制事件
```

删除

```javascript
不但从DOM树中删除了divs，而且还将事件删除divs=$("div").click(function(){})divs.delete()仅将DOM从DOM树中删除，不删除事件，重新放入时，事件依然存在divs.detach()清空divs的子元素divs.empty()
```

替换

```javascript
$("<p></p>").replcaeAll("div")  返回p$("div").replcaeWith("<p></p>"")
```

### 事件

```javascript
$("div").bind("click",function(){})$("div").unbind("click",function(){}) //删除事件$("div").on("click",function(){})$("div").off("click",function(){})  //删除事件$("div").one("click",function(){})  //只侦听一次//删除匿名函数触发的事件$("div").on("click.a",function(){    $("div").off("click.a")  //删除a事件  起别名的方式区别事件})简写：$("div").click(function(){    $("div").off("click")})//hover$("div").hover(function(){},function(){})  //第一个函数是鼠标经过时，第二个函数是鼠标离开时$(document).ready(function(){})  //页面使用DOM和渲染树合二为一了$(window).on("load",function(){})  //页面加载完毕，包括图片
```

鼠标事件

```javascript
$("div").on("click",参数,clickHandler)function clickHandler(e){    console.log(e.data) //这里的data就是触发改事件时传递过来的参数}$("div").click(参数,clickHandler)
```

事件抛发

```javascript
$("div").click(function(){})$("div").trigger("click")//抛发传参$("div").on("click",function(e,a,b){    console.log(e,a,b)})$("div").trigger("click",[a,b])$("div").triggerHandler("click",[a,b]) trigger和triggerHandler的区别1.trigger会触发默认行为，triggerHandler不会2.trigger会冒泡，triggerHandler不会3.trigger会影响到所有元素，triggerHandler只会影响第一个匹配到的元素4.trigger返回当前包含事件触发元素，triggerHandler会返回当前事件执行的返回值
```

### 动画

``` javascript
后面可以加回调函数$("div").hide(时间,function(){动画完毕执行})$("div").hide(时间).show(时间) 先隐藏再显示$("div").toggle(时间) 切换显示和隐藏$("div").slideUp(时间).slideDown(时间)  先上拉再下滑$("div").slideToggle(时间) 自动上拉和下滑$("div").fadeIn(时间).fadeOut(时间) 渐入渐出 $("div").fadeToggle(时间)$("div").animate({left:200},时间).animate({top:200},时间) //动画  可以连续动画                                                      
```

### 插件和AJAX

插件

```javascript
$.extend({	randomColor:function(){        return Array(6).fill(1).reduce((v,t)=>{            return Math.floor(Math.random()*16).toString(16)        },"#")    }}); //如果后面紧跟闭包函数，则必须需要加上分号; (function(){    $.fn.bgc=function(color){      if(color===undefined)  return this.css("backgroundColor")      this.css("backgroundColor",color);      return this;   }})();$("div").width(50).height(50).bgc("red");console.log($("div").bgc());//使用插件的步骤：1.使用闭包2.扩展：$.extend用于自身方法  $.fn.extend用于扩展jQuery类3.选择器
```

AJAX

```javascript
$.getJSON("json文件",function(){})$.getscript("js文件",function(){})$.getscript("js文件")  //加载js文件并执行//jsonpvar script=document.createElement("script")script.src="网址?传参"document.appendChild(script)$.getScript("网址?参数")  //和上面一样的效果$.get("网址",{参数},function(data){})$.post("网址",{参数},function(data){})$(document).load("网址/html文件"，{参数},function(data){})  //可以导入头部和尾部
```

```javascript
//$.ajax
$.ajax({    url:网址    type/method:方式    data:传递的数据    timeout:设置请求超时时间    dataType: 数据类型 json,jsonp,html等     beforeSend:    complete:    success:    error:    cache:    content:	contentType:    async:    jsonp:    .    .    .})
```

