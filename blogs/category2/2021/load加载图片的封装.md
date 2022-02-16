---
title: load加载图片的封装
date: 2021-5-2
tags:
 - tag4
categories: 
 - JS-node
---

# load加载图片的封装

```javascript
var Utils = (function(){
    LOAD_FINISH_IMG:'load_finish_img'
    return {
        loadImage:function(sourceArr,finishHandler,basePath,suffix){
            if(typeof sourceArr==="string") sourceArr=[sourceArr]
            if(basePath&&typeof basePath==="string"){
                basePath=basePath.endsWith("/")?basePath:basePath+"/"
                sourceArr=sourceArr.map(function(item){
                    item=String(item)
                    return basePath+(item.startsWith("/")?item.slice(1):item)
                })
            }
            if(suffix&&typeof suffix==="string"){
                sourceArr=sourceArr.map(function(item){
                    item=String(item)
                    if(![item.endsWith(-5,-4),item.endsWith(-4,-3)].inculdes("."))item+=suffix
                    return item
                })
            }
            var img=new Image()
            img.src=sourceArr[0]
            img.n=0;
            img.finishList=[]
            img.sourceArr=sourceArr
            img.finishHandler=finishHandler
			img.addEventListener("load",loadHandler)
            img.addEventListener("error",errorHandler)
        },
        loadHandler:function(e){
            this.finishList.push(this.cloneNode(false))
            if(Utils.loadImg(this)) return 
        },
        errorHandler:function(e){
			this.finishList.push(null)
            if(Utils.loadImg(this)) return 
        },
        loadImg:function(img){
            img.n++
            if(img.n>img.sourceArr.length-1){
                img.removeEventListener("load",loadHandler)
            	img.removeEventListener("error",errorHandler)
                if(typeof img.finishHandler==="Function") img.finishHandler(img.finishList.length===0?img.finishList[0]:img.finishList)
                else{
                    var evt=new Event(Utils.LOAD_FINISH_IMG)
                    evt.finishList=img.finishList
                    document.dispatchEvent(evt)
                }
                return true
            }
            img.src=img.sourceArr[img.n]
            return false
        }
        
    }
})()
```