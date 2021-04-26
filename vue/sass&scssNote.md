//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info

#### sourcemap的作用

```
  最近在使用gulp构建项目，在编译sass的时候遇到了sourcemaps，查阅了相关资料，大概弄懂了它是个神马，以及如何生成使用。

       首先，从名字可以看出sourcemaps是生成文件到源文件的一个映射，也就是sourcemaps记录了生成文件中的每一条语句在源文件中的对应位置。以gulp编译sass为例（假设你对gulp已经有了一定了解）：

1. 先安装gulp-sourcemaps，命令为：npm install --save-dev gulp-sourcemaps

2. 在gulpfile.js中引用它：sourcemap = require( 'gulp-sourcemaps' )

3. 建立一个任务

gulp.task( 'sass', function() {
  return gulp.src( ['./src/css/index.scss'] )  //后缀为scss
    .pipe( sourcemap.init() ) //初始化
    .pipe( sass({outputStyle: 'compressed'}) )
    .pipe( sourcemap.write( './maps' ) ) //生成sourcemap文件，路径为./maps
    .pipe( gulp.dest( './des/dist/' ) )
} );

这样在命令行中运行该任务：gulp sass，就可以生成sourcemaps文件了



在html中引入生成的css文件，谷歌浏览器打开该html文件，我们就能够看到下图。

标红的部分可以看到对应的样式文件是scss，点击进入就能够找到这个样式对应在scss文件中的位置了。

```

<img src="imgs\sass scss sourcemap20161018131453040.png" style="zoom: 150%;" />







四种编译风格：
1.nested（默认，最后一行包括}）
2.expanded(传统CSS样式)
3.compact（不同的选择器会单独压缩在一行）
4.compressed（完全压缩）

可以写相对路径



