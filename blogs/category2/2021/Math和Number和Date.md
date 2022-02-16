---
title: Math和Number和Date
date: 2021-5-4
tags:
 - tag4
categories: 
 - JS-node
---

# Math和Number和Date

## 1. Math

#### Math的静态方法

```javascript
1.Math.e (2.718)
2.Math.LN2
3.Math.LN10
4.Math.LOG2E
5.Math.LOG10E
6.Math.PI
7.MATH.SQRT1_2
8.Math.SQRT2
```

#### Math的方法

```
1.Math.abs() 绝对值
2.Math.floor() 向下取整
3.Math.ceil() 向上取整
4.Math.round() 四舍五入取整 
注意：   Math.round(-3.5) // -4+0.5 => -4+1 => -3
		Math.round(-3.2) // -4+0.8 => -4+1 => -3
		Math.round(-3.7) // -4+0.3 => -4+0 => -3
5.Math.max() 求最大值
6.Math.min() 求最小值
```

```javascript
求数组中的最大值和最小值
1.Math.max.qpply(null,[1,2,3,6,9])
  Math.min.apply(null,[1,2,3,6,9])
2.var obj=arr.reduce(function(value,item){
    if(value.min===undefined) value.min=item
    if(value.max===undefined) value.max=item
    if(value.min>item) value.min=item
    if(value.max<item) value.max=item
    return value
})
```

```javascript
7.Math.pow(数值，幂次方) 求幂
8.Math.sqrt() 求平方根
9.Math.random() 随机数 0~1
```

```javascript
求随机颜色
1.function getRandomColor(){
    return Array(6).fill(1).reduce(function(value,item){
        return value+=~~((Math.random()*16).toString(16))
    },"#")
}
```

```javascript
随机数组
var arr=Array(100).fill(1).reduce(function(value,item,index){
	return index
})
arr.sort(function(item){
    return Math.random()-0.5
})
```

## 2. Number

#### Number常量

```javascript
1.Number.NaN =>NaN
2.Number.NEGATIVE_INFINITY negative_infinity
3.Number.POSITIVE_INFINITY positive_infinity
4.Number.MAX_VALUE>0
5.Number.MIN_VALUE>0
```

#### Number方法

```javascript
1.Number.toString()
2.Number.toFixed() 保留小数点 会四舍五入
3.Number.toLacalString() 转换为本地数值
4.Number.toPrecision(数值) 科学计数法，保留几位数，只针对于大于零的数，从有数字开始向后保留
5.Number.toExponential(数值) 科学计数法，保留几位数，不限制正数负数，保留小数点后面几位,/*保留数小于位数时，会四舍五入*/
6.Number.isNaN()
7.Number.isInteger()
8.Number.isFinite() 判断是否有穷尽
9.Number.isSafeInteger()  数值安全范围 -(2^53-1)~(2^53-1)
```

## 3. Date

var date=new Date()

#### Date的静态方法：

```javascript
1.Date.now():获取毫秒数，从1970,1,1到现在的时间的毫秒数
			 UTC时间：格林尼治时间（正24区和负24区）
             中国处于格林时间的正8区
2.new Date().getTime() :时间戳 和Date.now()一样
```

#### Date的方法

```javascript
date.getFullYear()
date.getMonth() //0~11
date.getDate()
date.getDay() 0~6
date.getHours()
date.miuntes()
date.seconds()
date.getMilliseconds()

date.setFullYear()
.
.
.
date.setMilliseconds()
```









