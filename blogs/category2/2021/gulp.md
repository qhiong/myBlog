---
title: gulp
date: 2021-9-20
tags:
 - tag4
categories: 
 - JS-node
---
# gulp

### gulp3

package.json

![image-20211122192017247](C:\Users\yyh\AppData\Roaming\Typora\typora-user-images\image-20211122192017247.png)

这是gulp3的写法，不可以用做gulp4

```javascript
gulp.task("a",function(){
    console.log("aaa")
})
gulp.task("default",["a"],function(){
    console.log("default")
})

在终端输入：
npm init -y
npm i gulp@3 -D
导入gulp-load-plugins，gulp-concat，gulp-uglify，gulp-rename，gulp-minify-css，gulp-sass，sass
```

```javascript
var gulp=require("gulp");
// 可以使用这个去替代下面的包
var plugin=require("gulp-load-plugins")();
// 连接文件内容连接起来
// var concat=require("gulp-concat");
// 压缩文件
// var uglify=require("gulp-uglify");
// 给压缩好的文件重命名
// var rename=require("gulp-rename");
// 去掉重复的css选择器
// var minifyCss=require("gulp-minify-css");
var sass=require("gulp-sass")(require('sass'));

// 分配一个任务，在package.json文件中的scripts调试中添加“名”:"执行的gulp文件"
// gulp.task("b",function(){
//     console.log("bbb")
// })
// 在执行a任务之前执行任务
// gulp.task("a",["b"],function(){
//     console.log("abc");
// })
// 执行默认任务
// gulp.task("default",function(){
//     console.log("aaa")
// })

gulp.task("a",function(){
    // gulp.src("./src/**/*.js")
    // gulp.src("./src/**/*.*")
    // gulp.src("./src/js/*.js")
    // 将src中的[]文件进行打包
    gulp.src(["./src/js/b.js","./src/js/a.min.js"])
    // .pipe(concat("main.js"))
    .pipe(plugin.uglify())
    //将打包好的文件重命名
    .pipe(plugin.rename(function(file){
        // 根据file下的basename查看是否包含min，包含则直接打包，不包含则将文件名加上min之后再打包
        if(file.basename.includes(".min")) return file;
        file.basename+=".min";
        return file;
    }))
    // 将打包好的文件放在哪个文件下面
    .pipe(gulp.dest("./dist/js"));

    // gulp.src("./src/css/*.css")
    // .pipe(concat("main.css"))
    // .pipe(minifyCss({
    //     keepBreaks:true,//是否添加换行
    //     // advanced:false//是否合并相同选择器，默认true
    // }))
    // .pipe(rename("main.min.css"))
    // .pipe(gulp.dest("./dist/css/"))

    gulp.src("./src/scss/*.scss")
    .pipe(sass())
    .pipe(plugin.concat("main.css"))
    .pipe(plugin.minifyCss({
        keepBreaks:true,//是否添加换行
        // advanced:false//是否合并相同选择器，默认true
    }))
    .pipe(plugin.rename("main.min.css"))
    .pipe(gulp.dest("./dist/css/"))
})


gulp.task("default",function(){
    gulp.watch("./src/scss/*.scss",function(){
        gulp.src("./src/scss/*.scss")
        .pipe(sass())
        .pipe(plugin.concat("main.css"))
        .pipe(plugin.minifyCss({
            keepBreaks:true,//是否添加换行
            // advanced:false//是否合并相同选择器，默认true
        }))
        .pipe(plugin.rename("main.min.css"))
        .pipe(gulp.dest("./dist/css/"))
    })
})
```

### gulp4

##### 将gulp3升级

```javascript
var gulp=require("gulp");
// gulp4在执行任务时必须要执行done函数
gulp.task("a",function(done){
    console.log("aaa")
    done();
})
// 在默认执行的文件前先执行a文件；但是是错误的！！无法运行
gulp.task("default",["a"],function(done){
    console.log("default");
    done();
})
// 串行执行
gulp.task("default",gulp.series(["a"],function(done){
    console.log("default");
    done();
}))
// 并行执行
gulp.task("default",gulp.parallel(["a"],function(done){
    console.log("default");
    done();
}))
gulp.task("default",function(done){
    //监听文件js改变，改变后进行一次打包
    gulp.watch("./src/js/*.js",function(finish){
        gulp.src("./src/js/*.js")
        .pipe(gulp.dest("./dist/js/"))
        .on("end",finish);
    })
})


// 使用promise来执行gulp打包
gulp.task("b",function(){
    return new Promise(function(resolve,reject){
        console.log("bbb");
        resolve();
    })
})

gulp.task("default",gulp.series(["b"],function(done){
    console.log("default");
    done()
}))

function a(done){
    console.log("aaa");
    done();
}
function b(done){
    console.log("bbb");
    done();
}

function c(done){
    console.log("ccc");
    done();
}
exports.a=a;
exports.c=c;
//可以将abc三个任务同时打包出去，但是a,b比c先执行
exports.default=gulp.series([a,b],c);
```

##### 用gulp4执行打包

```javascript
const gulp=require("gulp");
const {src,dest,series,watch}=require("gulp");
const {concat,uglify,rename,babel,minifyCss}=require("gulp-load-plugins")();
const sass=require("gulp-sass")(require("sass"));
const browser=require("browser-sync")

function changeJs(done){
    src(["./src/js/b.js","./src/js/**/*.js"])
    .pipe(babel({
        presets: ['@babel/env']
    }))
    .pipe(concat("main.js"))
    .pipe(uglify())
    .pipe(rename("main.min.js"))
    .pipe(dest("./dist/js"))
    .on("end",browser.reload)
    done();
}

function changeCss(done){
    src(["./src/scss/*.scss","./src/css/*.css"])
    .pipe(sass())
    .pipe(concat("main.css"))
    .pipe(minifyCss())
    .pipe(rename("main.min.css"))
    .pipe(dest("./dist/css"))
    .on("end",browser.reload);
    done();
}

function changeHTML(done){
    browser.reload();
    done();
}

function init(done){
    browser.init({
        "port":"4010",
        "server":"./"
    });
    watch("./src/js/*.js",changeJs);
    watch("./src/css/*.css",changeCss);
    watch("./src/scss/*.scss",changeCss);
    watch("./**/*.html",changeHTML);
    done();
}
exports.default=series([changeJs,changeCss,changeHTML],init);

```


