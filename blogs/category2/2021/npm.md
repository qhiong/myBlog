---
title: npm
date: 2021-9-17
tags:
 - tag4
categories: 
 - JS-node
---

# npm

####  node package manager

```javascript
npm init 初始化配置 //在初始化过程中会产生很多提示内容，因此可以采用 npm init -y来自动确认默认消息
执行完初始化配置之后，会在当前文件夹下生成一个新的package.json配置文件
这个package.json文件的作用：
1.可以把当前的项目上传到npmjs官方网站的库里，为所有人提供当前项目的共享，这个文件夹就是上传需要的配置文件。
2.在执行node时，通过这个配置文件的命令来执行node代码，完成传参等需要
3.项目中将会使用大量其他包（插件），这些包对于当前这个项目来说就是依赖，这些依赖配置需要分门别类进行归纳，以方便再次更新对应包，在项目上线前做好打包时对于依赖包进行确认打包。
4.用于处理使用ES6模块化
在nodejs这种，使用type="module" ES6模块化，需要将文件的扩展名改为.mjs
```

#### package.json文件

```javascript
name:项目名，一般不使用数字，不允许使用大写；使用-/@三个来区分每个单词，//npmjs库非常庞大，所以需要进行区分
version:版本号；当前项目的版本
例如1.2.3====》1代表大版本，指大的结构发生变化时，修改大版本
			  2代表中小版本，指代码需要迭代新的内容时
              3代表微版本，修改各版本的bug,优化性能
description：描述，描述这个包的使用作用，以方便被用户搜索到。
main:执行文件的入口文件
scripts：所有脚本的集合
keywords:关键词；这个包在别人搜索该关键词时可以被找到
author:作者；
license:版权证书；
dependencies:项目依赖
devDependencies:开发依赖
```

##### npm 下载插件

npm i 插件名 -g  ===> 这个插件主要适用于命令类型插件，安装在node所在系统文件夹下，cli就是命令类型插件

**nrm** 切换npm下载镜像源

yarn和npm类似，也是包管理器

yarn支持断点（断网之后能够保持当前下载的位置）下载，npm不支持

npm i anywhere -g ===>web服务工具;类似于live serve

npm i http-server -g  ===> web服务工具，可以做代理

npm i nodemon -g ===>如果修改了node文件，自动重新执行node文件

**npm安装依赖插件**：此时安装的都是在当前文件夹下的node_modules文件夹下

npm i 插件名 --save/-S ===> 安装项目依赖插件；项目上线后，运行任然需要使用的插件

npm i 插件名 --save-dev/D ===>安装开发依赖插件，在开发时使用；项目上线后，不再需要，比如：打包工具；测试工具

npm i jquery -S  ===> js中DOM的快速开发插件

npm i lodash -S ===> 可以获取很多数组，对象，函数，字符串等方法，直接使用

npm uninstall 插件名 ===>删除插件

清除缓存：npm cache verity

强制清除缓存：npm cache clean --force

出现ErrorNo --4048错误时，需要上面来进行清除