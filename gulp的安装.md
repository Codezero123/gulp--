###gulp插件下载地址：www.npmjs.com
###安装gulp
- 通过npm安装："npm install gulp-cli -g"
                <!--下面这种方法也可以使用-->
                "npm install gulp -g"

### gulp使用
- 1.在当前项目中也要安装gulp:'npm install gulp --save'（代表保存了当前版本号）
- 2.还需要在当前项目中新建一个文件：gulpfile.js
- 在里面内容写:
        var gulp  = require('gulp');
        <!--开始任务：-->
        gulp.task('test',function(){
            console.log(123);
        })
- 3.执行任务：'gulp 任务名'
    一定要在gulpfile.js所在的文件夹下打开cmd;
    + 示例：'gulp test'
- 4.处理app.js文件，讲文件移动到指定位置
- gulp.task('script',function(){
        <!--找到源文件路径-->
        gulp.src('./app.js')
        <!--指定输出路径将文件移动过去-->
        .pipe(gulp.dest('./dist'))
        })
### 对js进行压缩
- 先下载压缩插件'npm install gulp-uglify --save'
- 再在gulpfile.js中进行操作
    var uglify  = require('gulp-uglify');
        <!--开始任务：-->
        gulp.task('test',function(){
            gulp.src('./*.js')
            .pipe(uglify())
            .pipe(gulp.dest('./main'))
            })
### 对js进行合并
- 下载合并插件'npm install gulp-concat --save'
-  再在gulpfile.js中进行操作
    var uglify  = require('gulp-concat');
        <!--开始任务：-->
        gulp.task('script',function(){
            gulp.src(['./app.js','./sign.js'])
            .pipe(concat('index.js'))
            .pipe(uglify())
            .pipe(gulp.dest('./dist'))
            })
### 对css进行压缩操作
- 'npm install gulp-cssnano --save' 
-  再在gulpfile.js中进行操作
    var cssnano  = require('gulp-cssnano');
        <!--开始任务：-->
        gulp.task('style',function(){
            gulp.src(['./app.css','./sign.css'])
            <!--合并文件-->
            .pipe(concat('index.css'))
            <!--压缩文件-->
            .pipe(cssnano())
            <!--放到指定文件夹-->
            .pipe(gulp.dest('./dist'))
            })
### 对html进行压缩操作
- 'npm install gulp-htmlmin --save'
- 再在gulpfile.js中操作
    var htmlmin = require('gulp-htmlmin');
    gulp.task('html',function(){
        gulp.src(['./index.html'])
        <!--htmlmin(括号内部必须传入参数,具体可以传入哪些需要上网查)-->
        .pipe(htmlmin({collapseWhitespace:true}))
        .pipe(gulp.dest('./dist'))
        })
### gulp.watch自动监视文件变化，执行相应任务（watch,和run基本不会使用）
- gulp.run,直接执行指定任务（一般需要加上，否则不能监听开启监听之前所做的改变）
- 在gulpfile.js中操作
    gulp.task('mywatch',function(){
        <!--首先执行一次-->
        gulp.run('script')
        <!--监视js文件的变化，然后执行script任务-->
        <!--第一个参数：要监视的文件规则-->
        <!--第二个参数：要执行的任务-->
        gulp.watch(['./app.js',sign.js],['script'])
        })
