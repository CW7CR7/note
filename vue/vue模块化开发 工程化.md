commonJS

也就是node.js中用的语法

1. 模块为单文件模块和包
2. 模块成员导出：module.exports和exports
3. 模块成员导入：require('模块标识符')



common.js只适用于服务器端，amd,cmd只适用于浏览器端



### ES6模块化整合了上述的优点

每个Js文件都是一个独立的模块

导入成员用import关键字

暴露成员用export关键字



1. cnpm i --save-dev @babel/core @babel/cli @babel/preset-env @babel/node

2. cnpm i --save @babel/polyfill

3. 项目根目录创建babel.config.js

4. 在创建的文件里写

   ```js
   const presets = [
     [
       "@bebel/env",
       {
         targets: {
           chrome: "67",
           edge: "17",
           firefox: "60",
           safari: "11.1",
         },
       },
     ],
   ];
   module.exports = { presets };
   
   ```

   5.npx babel-node index.js



node xxx.js

运行文件 后缀js可以省去



1. package.json的作用：复用
2. 通过npm i就可以直接把package.json里面的依赖下载下来
3. 为什么不复制node_modules，因为文件数量太多，复制速度太慢

### cnpm国内镜像

npm i -g  cnpm --registry=https://registry.npm.taobao.org



#### 下载多个依赖：空格直接隔开

cnpm i jquery vue redis mysql

指定版本号：

cnpm i redis@3.0.2

卸载：

npm uni jquery

下载babel:

cnpm i -g babel-cli

查看babel版本

babel --version

#### 小知识：map方法：

map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

map() 方法按照原始数组元素顺序依次处理元素。

**注意：** map() 不会对空数组进行检测。

**注意：** map() 不会改变原始数组。

```js
在map的参数写改变数组的每一项的方法
arr=arr.map(item=>item+1)
```



1. 在项目根目录创建.babelrc文件

2. 配置.babelrc  这个文件是babel的依赖文件

   ```json
   {
       "presets":["es2015"],
       "plugins": []
   }
   ```

3. cnpm i --save-dev babel-preset-es2015
   这是一个转换器，很大

4. babel src -d dist 
   src\example.js -> dist\example.js 然后就生成了转换后的文件

   ```cmd
   --out-file或者-o 指定输出文件
   babel src/abc.js -o dist/abc.js
   整个目录都转换
   --out-dir或者-d 指定输出目录
   把src文件夹转换至dist文件夹
   babel src -d dist
   ```

   



#### package.json里面自定义指令 在scripts里面设置

```json
{
  "name": "npmModularity",
  "version": "1.0.0",
  "description": "",
  "main": "redisdb.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
      "dev":"babel src -d dist"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-preset-es2015": "^6.24.1"
  }
}

```

npm run dev运行（这里要注意:dev是自定义指定名字当然你在scripts对象里面把命令键名写成a就可以npm run a来执行这个命令）

### commonJS语法

运算.js  暴露：

```js
module.exports={
    //a1是暴露出的名字，sum是该js文件的其中的一个方法名
    a1:sum
}
```

导入：

```js
const m=require('./运算.js')
此时,m就是一个对象
m.sum()
```

### ES6语法 更像java

reduce方法

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<p>点击按钮后对数组元素进行四舍五入并计算总和。</p>
<button onclick="myFunction()">点我</button>

<p>数组元素之和: <span id="demo"></span></p>

<script>
var numbers = [15.5, 2.3, 1.1, 4.7];

function getSum(total, num) {
    //total是之前的累加之和
    return total + Math.round(num);
}
function myFunction(item) {
    document.getElementById("demo").innerHTML = numbers.reduce(getSum, 0);
}
</script>

</body>
</html>
```



导入方法

```js
import {
    sum:sum
} from './运算.js'
```

如果直接执行node src/example则会报错： 这是因为import是ES6语法

SyntaxError: Cannot use import statement outside a module

1.转换成ES5代码：

babel src -d dist

2.此时执行就可以了：

node dist/example



```js
暴露：
function sum(a,b){
    return a+b
}
function sub(a,b){
    return a-b
}
// commonJS语法 node用的 注意：暴露的语法只支持写一种
// module.exports={
//     sum:sum,
// }
export {
    // sub:sub  这样写是错误的，因为别称是归导致者定义的
    sub,sum
}


```

```js
引入
import {sum,sub} from './testTools'
console.log(sum(1,10));
console.log(sub(1,10));
```

```js
暴露对象写法：
// 当然，用得最多的暴露方法是：
export default{
    // 注意在默认暴露对象里面不能加function名字
    // function mul(a,b) {
    //     return a*b
    // },
    // 正确写法：
     mul(a,b) {
        return a*b
    },
}
```

```js
引入对象写法：
// 符合编程逻辑的导出，也是用得最多的
import hisTools from './testTools2'
console.log(hisTools.mul(2,10));
```

## node和jdk

<img src="./imgs\jdk和node的异曲同工之妙Snipaste_2021-03-04_23-28-00.jpg" style="zoom:67%;" />

js是解释性语言，所以不需要编译，直接运行即可

#### node操作mysql

```js
const mysql = require("mysql");
// 配置数据连接信息
var thisConnection = mysql.createConnection({
  host: "127.0.0.1",
  port: 3306,
  user: "root",
  password: "root",
  database: "myemployees",
});
// 开启连接
thisConnection.connect();
// 查询 第二个参数 回调函数，里面形参随便写
thisConnection.query(
  "select AVG(`hour`) as avgTime FROM `working-time3`",
  (error, results, fields = 0) => {
    // thisConnection.query("select * FROM working-time3",(err,res,fields)=>{
    if (error) throw error;
    console.log("查询结果：" + results);
  }
);
// 关闭连接
thisConnection.end();

```



#### node全局安装位置：

npm config ls 

其中：prefix=C:\Users\Administrator\AppData\Roaming\npm就是我们全局安装了哪些方法的地方

 这时可以通过命令来更改路径

```
npm config set prefix E:\
```

##### 第一个node服务器小demo

```js
// node安装时自带http模块
const thisHttp = require("http");
thisHttp
  .createServer((request, response) => {
    // 浏览器怎么认识this is server 以text/html形式解析数据
    response.writeHead(200, { "Content-type": "text/html" });
    response.end("<h1>this is server</h1>");
  })
  .listen(81);
console.log("81端口已经启动");

```



## webpack

### webpack执行步骤

#### 打包步骤

安装webpack:

cnpm i -g webpack webpack-cli

查看Webpack版本：

webpack -v

1. 创建一个项目目录，然后npm init -y

2. 创建一个src目录

3. 在src里面创建需要合并的util.js和common.js

   ```js
   common.js文件
   exports.info=function (str) {
       console.log(str);
       document.write(str)
   }
   ```

   ```js
   tools.js文件
   exports.add2=function (a,b) {
       return a+b*2
   }
   ```

   

4. 准备一个入口文件main.js，其实就是模块的集中引入

   ```js
   // 入口文件
   const util=require('./tools')
   const common=require('./common')
   console.log(common.info('carlos'));
   console.log(util.add2(1,2));
   ```

   

5. 在根目录定义个webpack.config.js配置打包的规则 注意：必须要放在根目录下才可以

   ```js
   // 安装node时候就提供了path模块 所以就不需要再次的下载
   const path=require('path');
   // 定义打包规则
   module.exports={
       // 入口文件
       entry:path.join(__dirname,'./src/main.js'),
       // 输出文件
       output:{
           // __dirname就是当前项目根目录
           path:path.resolve(__dirname,'./dist'),
           filename:'webpackDabao.js'
       }
   }
   ```

   

6. 执行Webpack cmd直接输入webpack回车即可
   其实这也是一个语法糖，真正的写法应该是webpack -config webpack.config.js



#### webpack监听：

cmd  webpack -w

#### webpack打包css文件

因为webpack默认只打包js文件，所以需要配置后才能打包css文件

#### 步骤：

1. cnpm i --save-dev style-loader css-loader

2. 修改webpack.config.js

   ```js
   // 安装node时候就提供了path模块 所以就不需要再次的下载
   const path=require('path');
   // 定义打包规则
   module.exports={
       // 入口文件
       entry:path.join(__dirname,'./src/main.js'),
       // 输出文件
       output:{
           // __dirname就是当前项目根目录
           path:path.resolve(__dirname,'./dist'),
           filename:'webpackDabao.js'
       },
       module:{
           rules:[{
               // 打包css文件
               test:/\.css$/,
               use:['style-loader','css-loader']
           }]
       }
   }
   ```

3. cmd webpack即可

##### webpack也是一种打包思想

uniapp,vue项目乍看起来没有Webpack。实际上呢，他们都已经内置了类似于webpack的工具

#### 以vue-element-admin项目举例

main.js -> 入口文件

App.vue->入口页面 和index页面进行绑定

api->调用接口用的

所有视图都在views文件夹下面

npm指令：几乎都有的nodejs项目指令都是：

1. npm run dev 开发运行
2. npm run build 打包



### vue脚手架 vue-cli

更加简化了webpack的操作，使得开发更加的高效

#### vue-cli安装步骤

1. npm i -g @vue/cli --registry=https://registry.npm.taobao.org
   推荐装3版本的vue-cli，3版本可以创建3版本也可以创建2版本的项目
2. 查看安装的版本号
   vue -V
   显示：@vue/cli 4.5.11（21.3.8）



#### vue-cli脚手架创建项目的三种方式（前两种用的最多）

1. 基于交互命令行的方式，这个创建的是vue3的项目
   vue create projectName

2. 基于图形化界面
   1.vue ui
   2.然后进入创建，选择目录
   3.选择一套预设的时候，可以用vue提供的，也可以用自己的模板方式。 
   4.choose vue version,babel,router,linter/formatter,使用配置文件这几项要打开。
   5.pick a linter/formatter config选择eslint+standard config
   6.任务面板中的serve就是开发，build就是生产
   7.更改项目的端口号以及运行后自动打开浏览器:配置package.json文件，新增vue对象

   ```json
   {
     "name": "vue_ui_demo2",
     "version": "0.1.0",
     "private": true,
     "scripts": {
       "serve": "vue-cli-service serve",
       "build": "vue-cli-service build",
       "lint": "vue-cli-service lint"
     },
     "dependencies": {
       "core-js": "^3.6.5",
       "vue": "^3.0.0",
       "vue-router": "^4.0.0-0"
     },
     "devDependencies": {
       "@vue/cli-plugin-babel": "~4.5.0",
       "@vue/cli-plugin-eslint": "~4.5.0",
       "@vue/cli-plugin-router": "~4.5.0",
       "@vue/cli-service": "~4.5.0",
       "@vue/compiler-sfc": "^3.0.0",
       "@vue/eslint-config-standard": "^5.1.2",
       "babel-eslint": "^10.1.0",
       "eslint": "^6.7.2",
       "eslint-plugin-import": "^2.20.2",
       "eslint-plugin-node": "^11.1.0",
       "eslint-plugin-promise": "^4.2.1",
       "eslint-plugin-standard": "^4.0.0",
       "eslint-plugin-vue": "^7.0.0-0"
     },
     "vue":{
       "devServer":{
         "port":80,
         "open":true
       }
     }
   }
   
   ```

   但是呢，不推荐这种方式，因为package.json是用来管理包的配置信息。所以为了方便维护，推荐将vue脚手架的相关配置单独定义到vue.config.js文件中。在项目根目录创建vue.config.js文件:**两种配置方式二选一**

   ```js
   module.exports={
     devServer:{
       open:true,
       port:81
     }
   }
   ```
   

npm run serve启动项目

npm run build生产项目

3. 基于vue-cli2.x的旧模板，创建旧版vue项目（用的比较少的方法）(目前vue-cli都是4版本了)
   npm i -g @vue/cli-init
   vue init webpack projectName （注意哦，项目名字不能有大写字母，所以要写projectname）

   1. 安装过程会问你use eslint to lint your code:是否用ESLint做代码检查
   2. set up unit tests:单元测试相关
   3. setup e2e tests with nightwatch 单元测试相关
   4. shold we run npm install for you after the project has been created创建完成后直接初始化

   

创建完成之后的步骤

1. 到了项目目录，npm i
2. npm run dev






cmd 之后 f:就可以进入F盘，不需要输入cmd

### elementUI

基于vue2.0的桌面端组件库

为什么选择elementUI?

```
从 标准、生态、成熟度、视觉 几个方面来说。Ant Design 在 标准、视觉 上更胜一筹，但是 ant-design-vue 相对比较年轻，成熟度上差 Element Ui 一些。Element-UI 是国内做 Vue 最早，也最成熟的一家。用户群体多，遇到问题基本都能解决。View UI（原 iView） -  国内 Vue 生态圈内的佼佼者，由公司进行维护。周边有 Admin Pro（付费授权）、Admin UI Pro（付费授权）等。Layui - 我们公司有大部分遗留代码都采用 Layui，给我感觉 标准和成熟度上较差，视觉上见仁见智，生态相对还可以（加上 jQuery lib），传统开发模式、上手快。如果传统开发模式我更推荐  bootstrap 生态

最近在踩antd for vue的坑，快速开发还是推荐elementUI，思维更贴近vue，antd只是把jsx那一套放到了vue来，不过vue3.0出了之后，大概率用antd更多了。

```

#### vue-elementUI安装步骤

一。命令行方式安装

1. npm i element-ui -S --registry=https://registry.npm.taobao.org 注意：最好用电脑的cmd，vscode的终端一般是用来执行git命令

2. 在src文件夹下的入口文件main.js里写上：import myElement from 'element-ui'，然后运行发现报错：Module Error (from ./node_modules/eslint-loader/index.js):解决办法。我们这个时候认为可能是图形化创建项目vue3版本的问题，我们尝试用vue2再试一试。（VUE3是21年才正式发布的）成功解决BUG。入口文件main如下

   ```js
   import Vue from 'vue'
   import App from './App.vue'
   import ElementUI from 'element-ui'
   import 'element-ui/lib/theme-chalk/index.css'
   
   Vue.config.productionTip = false
   Vue.use(ElementUI);
   new Vue({
     render: h => h(App),
   }).$mount('#app')
   
   ```

   

二。vue-ui方式安装

1. vue ui
2. 点击左上角下箭头，通过vue项目管理器，进入具体的项目配置面板
3. 点击插件->添加插件，进入插件查询面板
4. 搜索vue-cli-plugin-element并且安装
5. 配置插件，实现按需导入，从而减少打包后项目的体积
   会问你 how do you want to import element?回答：默认导入fully import,按需导入import on demand

如果是ui引入，则main会显示：

```js
import './plugins/element.js'
```



### vue后台商城项目

#### 初始化项目

用vue ui安装 ，在左侧的依赖中搜索axios，勾选上之后，安装依赖

配置下gitee。同时配置这台电脑的ssh秘钥（一个密钥只能对应一台硬件）

npm install --registry=https://registry.npm.taobao.org下载后台接口依赖

node app.js运行后台接口（js后缀名可以省略）

postman测试接口

postman中，Body配置传递信息

##### cookie和session和token

如果前后端不存在跨域问题，则用cookie,session,存在跨域则用token。

token的使用原理：客户端传递用户名和密码给服务器端，服务器端验证痛过之后发送一个token一并返回给客户端，然后客户端拿到服务器端发送的token，存储在本地。后续客户端再发送请求，会携带着这个token一并请求服务器端。服务器端验证这个token，这样服务器端就知道你是哪一个用户。



先做登录功能。

创建一个新的login分支 git checkout -b login

git branch查看所有分支，以及当前的分支

App.vue根组件盒子中必须要有内容

#### scoped属性

scoped表示这个只在该组件里生效，所以组件一般都会带上这个属性

```html


<style lang="scss" scoped>

</style>
```

需要在vue ui中安装依赖node-sass,sass-loader,style.loader

运行报错：bug

TypeError: this.getOptions is not a function

sass-loader版本太高导致的

1.npm uninstall sass-loader 

2.npm install less-loader@7.0.3 --registry=https://registry.npm.taobao.org

下载node-sass依赖一直失败，在网上也没找到解决办法，退而求其次，选择less。需要下载依赖：less,less-loader

下载Less-loader时候提示：peerDependencies WARNING less-loader@5.0.0 requires a peer of less@^2.3.1 || ^3.0.0 but less@4.1.1 was installed

所以卸载less，重新安装3.0.0的less。再安装less-loader。即可

npm --save和--save-dev

```html
 使用命令 --save 或者说不写命令 --save  ,都会把信息记录到 dependencies   中；

                      dependencies 中记录的都是项目在运行时需要的文件；

                     使用命令 --save-dev 则会把信息记录到 devDependencies  中；

                     devDependencies 中记录的是项目在开发过程中需要使用的一些文件，在项目最终运行时是不需要的；

                     也就是说我们开发完成后，最终的项目中是不需要这些文件的；
————————————————
版权声明：本文为CSDN博主「cvper」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/cvper/article/details/88728505
```



遇到BUG：Syntax Error: TypeError: this.getOptions is not a function bug的代码，但是试了也无效，说是是less-loader安装的版本太高，210310是8.0.0版本。我们先卸载，然后再安装：cnpm install -D less-loader@7.x(注意:使用less并不需要安装style-loader)



遇到了BUG：给父盒子设置了padding，左边有空格，右边溢出 解决方法

<img src="imgs\给父盒子设置了padding，左边有空格，右边溢出 解决方法Snipaste_2021-03-11_00-23-13.jpg" style="zoom:50%;" />

```css
 .login_form_container{
      position: absolute;
      bottom: 50px;
     儿子是100%宽度也是导致了这个BUG的元凶之一
      width: 100%;
      padding: 0 20px;
     设置成怪异盒子即可
      box-sizing: border-box;
    }
```





如果elementUI是按需导入的话，那么plugins文件夹的element.js需要这样写：

```js
import Vue from 'vue'
import {Button} from 'element-ui'
import {Form,FormItem} from 'element-ui'
Vue.use(Button)
Vue.use(Form)
Vue.use(FormItem)
```

#### 弹性盒子

```css
   .login_btn_container{
        // position: absolute;
        // right: 20px;
        display: flex;
      错误的写法
        // justify-content: end;
       正确的写法
        justify-content: flex-end;
      }
```

#### onchange事件触发条件

```html
这个onchange是怎么触发的呢？经过实验，大致是以下几个步骤

一、当input捕获到焦点后，系统储存当前值

二、当input焦点离开后，判断当前值与之前存储的值是否不等，如果为true则触发onchange事件
```

#### input框accept属性

```html
实例
1.accept="image/gif, image/jpeg"
2.accept="application/msword"
3.accept="application/pdf"
4.accept="application/poscript"
5.accept="application/rtf"
6.accept="application/x-zip-compressed"
7.accept="audio/basic"
8.accept="audio/x-aiff"
9.accept="audio/x-mpeg"
10.accept="audio/x-pn/realaudio"
11.accept="audio/x-waw"
12.accept="image/gif"
13.accept="image/jpeg"
14.accept="image/tiff"
15.accept="image/x-ms-bmp"
16.accept="image/x-photo-cd"
17.accept="image/x-png"
18.accept="image/x-portablebitmap"
19.accept="image/x-portable-greymap"
20.accept="image/x-portable-pixmap"
21.accept="image/x-rgb"
22.accept="text/html"
23.accept="text/plain"
24.accept="video/quicktime"
25.accept="video/x-mpeg2"
26.accept="video/x-msvideo"
```



#### jquery index

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <ul>
      <li class="li">jQuery判断当前元素是第几个元素示例</li>

      <li class="li">jQuery获取第N个元素示例</li>

      <li class="li">jQuery选择器示例</li>
    </ul>
  </body>
  <script src="./js/jQuery-2.1.4.min.js"></script>
  <script>
    $(".li").click(function () {
      var index = $("ul li").index(this);

      alert(index);
    });
  </script>
</html>

```



遇到的BUG：$(...)[0].attr is not a function

答案：一、问题分析：
$(…)[0] 返回的是一个dom对象
而 attr() 方法 只能被JQuery对象所使用

所以，可以用$(…).eq()



遇到的BUG：

```js
var fileReader1,fileReader0,fileReader2,fileReader3 = new FileReader(); 这样写错误
这样写才对
var fileReader0 = new FileReader();
var fileReader1 = new FileReader();
var fileReader2 = new FileReader();
var fileReader3 = new FileReader();
```





#### jQuery each循环

1. 在遍历DOM时，通常用$(selector).each(function(index,element))函数；
2. 在遍历数据时，通常用$.each(dataresource,function(index,element))函数。



#### vue 挂载axios，设置默认请求头

入口文件main.js

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import './assets/css/global.css'
import './assets/fonts/iconfonts/iconfont.css'
import axios from 'axios'
// 设置默认请求头
axios.defaults.baseURL='http://127.0.0.1:8888/api/private/v1/'
// 挂载到vue实例上。以后每一个vue实例可以通过this.$axios访问axios
Vue.prototype.$axios=axios;


Vue.config.productionTip = false
Vue.use(ElementUI)
new Vue({
  router,
  render: h => h(App)
}).$mount('#app')

```

login.vue

```js
 login: function() {
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) {
          return;
        }
        // 发送axios请求 axios POST请求里面不是一个对象
        // const result =await this.$axios.post("login", this.loginForm);
        // 这里推荐使用对象的解构,data是原本对象里面的一个属性
        const {data:result} =await this.$axios.post("login", this.loginForm);
        console.log(result);
        // console.log(result.meta.status);
        var status=result.meta.status;
        if(status!=200){
          console.log('登录失败');
        }
      });
    }
```





#### 关闭vue项目恶心的eslint校验功能

项目根目录 vue.config.js

```js
module.exports={
  devServer:{
    open:true,
    port:82
  },
  // 关闭ESlint校准
  lintOnSave:false
}

```



#### 引入阿里字体图标iconfonts

把选中的图标加入购物车，然后下载代码。

font-class是unicode使用方式的一种变种，主要是解决unicode书写不直观，语意不明确的问题。

与unicode使用方式相比，具有如下特点：

- 兼容性良好，支持ie8+，及所有现代浏览器。
- 相比于unicode语意明确，书写更直观。可以很容易分辨这个icon是什么。
- 因为使用class来定义图标，所以当要替换图标时，只需要修改class里面的unicode引用。
- 不过因为本质上还是使用的字体，所以多色图标还是不支持的。

使用教程：

第一步：拷贝项目下面生成的fontclass代码：

引入css文件

```js
//at.alicdn.com/t/font_8d5l8fzk5b87iudi.css
```

第二步：挑选相应图标并获取类名，应用于页面：

```css
<i class="iconfont icon-xxx"></i>
```

实例：

```html
<el-input placeholder="请输入密码"
            prefix-icon="iconfont icon-mima"></el-input>
```

遇到了bug，验证规则不生效：

```
v-model 和 :model 的区别问题（ v-model 通常是用于 input 的双向绑定，但是它不会向子组件传递数据； 而 ：model 表示绑定自定义的属性，它只是将父组件的数据传递给子组件，没有实现父子组件间的数据双向绑定）。我在 form 表单中使用了 v-model 所以出现了错误.
el-form-item 的 prop 值要与 v-model 的值保持一致，表单验证时就会验证 el-input 元素绑定的变量 loginForm.username 的值是否符合验证规则
附件官方prop使用说明
```

重置表单：

```js
methods: {
    reset:function(){
      this.$refs.loginFormRef.resetFields()
    }
  },
```



elementUI文档表单方法 form-methods

css选择器妙用 css3

```scss
div.item-content:nth-last-of-type(1){
                    display: flex;
                    justify-content: center;
                    // background-color: #ff0000;
                }
```

jquery自执行函数

$(function(){ //在这里写你的代码 });



1. localStorage是永久的，本地必须要删除才会删除
2. sessionStorage是绘画机制的，页面关闭就会删除

浏览器localstorage位置：

![](imgs\sessionstorage位置 localstorage位置Snipaste_2021-03-16_16-20-20.jpg)





#### 配置格式化校准文件的方式

在项目根目录创建：.prettierrc(注意，是json格式文件不可以加注释)。以便于符合eslint校准规范

```json
{
    // 结尾是否加;
    "semi":false
    // 是否使用单引号
    "singleQuote": true
}
```



根目录的.eslintrc.js是配置eslint校准方式的文件

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  extends: [
    'plugin:vue/essential',
    '@vue/standard'
  ],
  parserOptions: {
    parser: 'babel-eslint'
  },
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
#关闭空格校准
    'space-before-function-paren':0
  }
}

```

此时login页面已经完成，下一步，git分支合并

查看目前在哪个分支

git branch 

切换到master分支

git checkout master

合并分支

git merge login

第一次推送该分支

git push -u origin 分支名



#### axios拦截器

在入口文件设置拦截器axios

注意：use函数里面最终需要返回出去否则会报错：Uncaught (in promise) TypeError: Cannot read property 'cancelToken' of undefined    at throwIfCancellationRequested (dispatchRequest.js?5270:12)    at dispatchRequest (dispatchRequest.js?5270:24)

axios请求

```js
async getMenuList(){
      const {data:result}=await this.$axios.get('menus')
      console.log(result);
      if(result.meta.status!=200){return this.$message.error(result.meta.msg)}
      this.menuList=result.data
    }
```



左侧菜单我们实现时候发现点击一个一级菜单，所有的一级菜单全部展开了，这是因为每一个是和index属性有关，我们这里因为设置死了，所以所有的操控都一样了，我们可以设置成item.id，但是elementUI规定这个值必须是string ，所以我们可以设置成item.id+''

```html
<el-submenu index="1" v-for="item in menuList" :key='item.id'>
```



#### elementUI只保持一个子菜单打开

elementUI侧边栏在 **NavMenu导航菜单** 中找到文档

```html
unique-opened='true'这个属性不应该设置给
<el-submenu :index="item.id+''" v-for="item in menuList" :key='item.id' unique-opened='true'>
    而是应该设置给el-menu,同时应该注意unique-opened应该是动态绑定属性。如果只写unique-opened就等于:unique-opened='true'
```



这样写不对的：

```html
      <el-aside :width="isCollapse?250px:125px">
这样写才对： 250px应该是字符串
                <el-aside :width="!isCollapse?'250px':'75px'">

```



less默认值传入的方法

```less
.height(@h:18px) {//有默认值 18px; 
    height:@h;
}
```



#### elementUI作用域插槽

elementUI状态二次加工 el-table

```html
<el-table-column prop="mg_state" label="状态">
          <!-- 加工布尔值数据，所以用插槽 -->
          <template slot-scope="s">
            <!-- {{ s.row }} -->
              s.row是table里的el-table-column这一行对应的所有数据
            <el-switch
              active-color="#409eff"
              v-model="s.row.mg_state"
              inactive-color="#ccc"
            >
            </el-switch>
          </template>
        </el-table-column>
```



关闭vue项目热更新 webpack

配置vue.config.js

vue-cli升级到3之后，减少了很多的配置文件，将所有的配置项都浓缩到了vue.config.js这个文件中，所以学懂并会用**vue.config.js**文件**很重要，很重要，很重要**。重要的句子要加粗。

```js
module.exports={
  devServer:{
    open:true,
    port:82
  },
  // 关闭ESlint校准
  lintOnSave:false,
  // 是否开启热更新
  chainWebpack:config=>{
    config.resolve.symlinks(false);
  }
}
```



#### elementUI常用类名

1. 天蓝：primary
2. 红色：danger
3. 橙色：warning
4. 浅绿色：success
5. 灰色：info

按钮的大小size:额外的尺寸：`medium`、`small`、`mini`，通过设置`size`属性来配置它们。

```html
 <el-button size="medium">中等按钮</el-button>
```

分页elementUI

```html
:total="total"也可以写成:total="this.total"
<el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="this.queryInfo.pagenum"
        :page-sizes="[1, 2, 3, 4]"
        :page-size="this.queryInfo.pagesize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
      >
    <script>
        // 每一页展示多少条
    handleSizeChange(s) {
      // console.log(`每页 ${s} 条`)
      this.queryInfo.pagesize=s;
      this.getUsers()

    },
    // 跳转到第多少页
    handleCurrentChange(p) {
      console.log(`当前页: ${p}`)
      this.queryInfo.pagenum=p;
      this.getUsers()
    }
    </script>
    
```



#### elementUI自定义验证表单

```js
var checkEmail = (rule, value, callback) => {
      const regEmail = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+(\.[a-zA-Z0-9_-])+/
      if (!value) {
        return callback(new Error('邮箱不能为空'))
      }
      setTimeout(() => {
        if (regEmail.test(value)) {
          console.log(1);
          return callback
        }
        // 验证不通过
        console.log(2);
          第一种写法不通过，必须第二种
        // return new Error('请输入合法的邮箱！')
        callback(new Error('请输入合法的邮箱！'))
      }, 1000)
    }
#在规则里这样定义
email: [
          { required: true, message: '请输入邮箱', trigger: 'blur' },
        // 自定义验证规则
          { validator: checkEmail, trigger: 'blur' }
        ],
```





#### 模板字符串加变量

```js
`当前页: ${p}`
```



#### gitignore

忽略以copy.php为结尾的文件

```
*copy.php
```

```git
*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

删除用户

方法名字不能叫delete，起了这个名字没有起作用，换了deletUser就可以用了。



#### elementUI弹出框 确认框

```js
#里面必须这样写才能拿到confirm或者是cancel
var result=await this.$confirm('此操作将会永久删除该用户，是否继续？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).catch(e => {
          return e;
        })
        console.log(result);
    },
```



#### 提交user分支代码

1. git branch查看自己在哪个分支
2. git checkout -b user 创建user分支 并且切换到user分支上
3. git push -u origin user 第一次推送到user分支上 （这里的user表示远程仓库的分支名叫user）
4. git checkout master 切换到主分支上
5. git merge user
6. git push 保证主分支也是最新的，因为master分支已经有了，所以直接git push即可

#### 开始right分支代码

创建分支：

git checkout -b rights

提交并且创建远程分支：

git push -u origin rights



vue格式化 属性名换行 配置vscode setting.json

```js
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            "wrap_attributes": "auto",
        }
     },



 注： // 对属性进行换行。
    // - auto: 仅在超出行长度时才对属性进行换行。
    // - force: 对除第一个属性外的其他每个属性进行换行。
    // - force-aligned: 对除第一个属性外的其他每个属性进行换行，并保持对齐。
    // - force-expand-multiline: 对每个属性进行换行。
    // - aligned-multiple: 当超出折行长度时，将属性进行垂直对齐。

```

#### 展开运算符...

```javascript
 var result = this.$refs.treeRef.getHalfCheckedKeys()
      // console.log(result)
      var result2 = this.$refs.treeRef.getCheckedKeys()
      // console.log(result2)
      #result,result2都是数组
      keys = [...result, ...result2]
```



## VUE插件

由于elementUI自带的tree功能较少，所以改用第三方

#### [1.vue-table-with-tree-grid](https://github.com/MisterTaki/vue-table-with-tree-grid)

使用教程

1. ```
   npm i vue-table-with-tree-grid -S
   ```

全局用法：

```
import Vue from 'vue'
import ZkTable from 'vue-table-with-tree-grid'

Vue.use(ZkTable)
```

按需导入用法：

```
import Vue from 'vue'
import ZkTable from 'vue-table-with-tree-grid'

Vue.component(ZkTable.name, ZkTable)
```

#### 2.[vue-quill-editor](https://github.com/surmon-china/vue-quill-editor)

第一步：npm install vue-quill-editor  --save
第二步：入口文件 main

```js
import Vue from 'vue'
import VueQuillEditor from 'vue-quill-editor'

// require styles
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

Vue.use(VueQuillEditor, /* { default global options } */)
```

其中 `Vue.use(VueQuillEditor, /* { default global options } */)` 第二个参数是 `Quill` 的配置。在这里我只改了默认的 `placeholder` 提示语，所以最后一行应该是：

```js
Vue.use(VueQuillEditor, {
  placeholder: '请输入内容',
});
```



第三步代码中直接用：

```html
<template>
  <!-- bidirectional data binding（双向数据绑定） -->
  <quill-editor v-model="content"
                ref="myQuillEditor"
                :options="editorOption"
                @blur="onEditorBlur($event)"
                @focus="onEditorFocus($event)"
                @ready="onEditorReady($event)">
  </quill-editor>
 </template>

```

#### 3.lodash（提供一些比较麻烦的对象或者数组的方法比如深拷贝）

第一步

npm i lodash -D

第二步 入口文件

```js

<script>
 
import _ from ‘lodash'
 
export default{} 
 
</script>

```

#### 4.babel-plugin-transform-remove-console(build时候移除console)

1.npm install babel-plugin-transform-remove-console --save-dev

2.在babel.config.js文件的plugins数组里面新增

'transform-remove-console'

在babel.config.js文件中配置这样的：

```js
// 发布时候的插件
productPlugins:[]
if(process.env.NODE_ENV==='production'){
  productPlugins.push('transform-remove-console')
}
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset'
  ],
  plugins:[...productPlugins]
}

```





get请求的参数传递用params

#### elementUI BUG:删除最后一页数据时候，加载前面一页，但是页面上现实空页

```js
// 由于删除最后一页的最后一条数据会加载前一页并且显示空页的BUG，需要对请求数据进行加工
// 总页数
// 因为已经删除了一个数据，所以total需要减一,ceil向上取整数
let totalPage=Math.ceil((this.total-1)/this.queryInfo.pagesize);
// console.log(totalPage,345);
// 当前的页数如果大于了总页数，就选择总页数
this.queryInfo.pagenum=this.queryInfo.pagenum>totalPage?totalPage:this.queryInfo.num;
// 如果小于1页，就选择第一页
this.queryInfo.pagenum=this.queryInfo.pagenum<1?1:this.queryInfo.pagenum;
this.getCateList()
```



不要用params关键词当做变量名









#### vscode小技巧

ctrl+b打开侧边栏

vscode是微软2015年发布的

#### elementUI table

1. stripe属性：斑马纹

2. border：带边框

3. :data="rightsList"：绑定的数组数据

4. 想第一列做成有序列表：

   ```html
   <el-table-column
             type="index"
             label="#"
             width="180"
           > </el-table-column>
   ```

5. 如果有的列里面想放自定义插槽的话：

   ```html
    <template slot-scope='s'>
                 <el-tag v-if="s.row.level==='0'">一级</el-tag>
             <el-tag v-else-if="s.row.level==='1'" type="success">二级</el-tag>
             <el-tag v-else type="warning">三级</el-tag>
             </template>
   ```

6. 查看展开行里面插值表达式数据的样子

   ```html
   <!-- 展开行 -->
           <el-table-column type="expand">
             <template slot-scope="s">
               <pre>{{s.row}}</pre>
             </template>
           </el-table-column>
   ```

   

#### elementUI upload上传文件

查看图片上传到后台，是否上传成功

![](imgs\chrome查看图片上传成没成功Snipaste_2021-04-02_11-12-13.jpg)

案例：服务器临时存储图片的路径

<img src="imgs\案例：服务器临时存储图片的路径Snipaste_2021-04-02_11-43-42.jpg" style="zoom:67%;" />





## 项目优化

### 生成文件报表

vue-cli-service build --report 

--report选项可以生成report.html以帮助分析打包内容

vue-cli的命令选项可以生成打包报告

当然也可以通过UI面板来生成这个报告（vue ui）



### 修改入口文件

1. chainWebpack通过链式编程，来修改webpack配置
2. configureWebpack通过操作对象，来修改webpack配置

设置dev和prod的入口文件 （也就是设置开发入口文件和生产入口文件）

vue.config.js

```js
module.exports = {
  devServer: {
    open: true,
    port: 82
  },
  // 是否开启ESlint校准
  lintOnSave: false,
  // 是否开启热更新
  chainWebpack: config => {
    config.resolve.symlinks(true);
  },
  // 修改入口文件
  chainWebpack: config => {
    config.when(process.env.NODE_ENV === 'production', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-prod.js')
    }
    )
    config.when(process.env.NODE_ENV === 'development', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-dev.js')
    }
    )
  }




}

```

### externals

默认情况下通过import语法导入第三方依赖包，最终会被打包合并到同一个文件中，从而导致打包成功后，但文件体积过大。

所以呢，可以通过webpack的externals节点，来配置并加载外部的CDN资源。凡是声明在externals中的第三方依赖包，都不会被打包

其实为了就是减少js/chunk-vendors.js文件的大小

vue.config.js

```js
module.exports = {
  devServer: {
    open: true,
    port: 82
  },
  // 是否开启ESlint校准
  lintOnSave: false,
  // 是否开启热更新
  chainWebpack: config => {
    config.resolve.symlinks(true);
  },
  // 修改入口文件
  chainWebpack: config => {
    // 发布模式
    config.when(process.env.NODE_ENV === 'production', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-prod.js')
      // 减少打包容量 webpack中的一个功能
      config.set('externals',{
        vue:'Vue',
        'vue-router':'VueRouter',
        axios:'axios',
        lodash:'_',
        echarts:'echarts',
        nprogress:'NProgress',
        'vue-quill-editor':'VueQuillEditor'
      })
    }
    )
    // 开发模式
    config.when(process.env.NODE_ENV === 'development', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-dev.js')
    }
    )
  }




}

```

同时public/index.html文件需要引入js文件

### 为项目设置动态的标题 title

vue.config.js:

```js
module.exports = {
  devServer: {
    open: true,
    port: 82
  },
  // 是否开启ESlint校准
  lintOnSave: false,
  // 是否开启热更新
  chainWebpack: config => {
    config.resolve.symlinks(true);
  },
  // 修改入口文件
  chainWebpack: config => {
    // 发布模式
    config.when(process.env.NODE_ENV === 'production', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-prod.js')
      // 减少打包容量 webpack中的一个功能
      config.set('externals',{
        vue:'Vue',
        'vue-router':'VueRouter',
        axios:'axios',
        lodash:'_',
        echarts:'echarts',
        nprogress:'NProgress',
        'vue-quill-editor':'VueQuillEditor'
      })
      # 判断title是否加prod-前缀
      config.plugin('html').tap(args=>{
        args[0].isProd=true;
        return args;
      })
    }
    )
    // 开发模式
    config.when(process.env.NODE_ENV === 'development', config => {
      // 首先清空默认main入口，再设置入口
      config.entry('app').clear().add('./src/main-dev.js')
      # 判断title是否加prod-前缀。开发模式就不加，发布模式就加上去
      config.plugin('html').tap(args=>{
        args[0].isProd=false;
        return args;
      })
    }
    )
  }
}

```



public/index.html:

```html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>bitbug_favicon.ico">
    <title><%= htmlWebpackPlugin.options.isProd?'':'dev-' %>后台管理系统</title>
    <% if(htmlWebpackPlugin.options.isProd){ %>
      <!-- 各种CDNlink script -->
      <link rel="stylesheet" href="">
      <script src=""></script>
      <% } %>
  </head>
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>

```

![](D:\work\jianGuoYun\work\demo\vue\imgs\实现效果Snipaste_2021-04-10_23-16-06.jpg)

![](D:\work\jianGuoYun\work\demo\vue\imgs\实现效果Snipaste_2021-04-10_23-18-44.jpg)



![](imgs\externals引入公共的js文件 线上文件Snipaste_2021-04-09_23-57-55.jpg)





同时public/index.html文件需要引入css文件，其他地方的导入css的代码就可以删掉了

<img src="D:\work\jianGuoYun\work\demo\vue\imgs\public index.html需要引入css Snipaste_2021-04-10_00-08-19.jpg" style="zoom:67%;" />



### 路由懒加载



打包构建项目时候，JS包会变得非常的大，这样呢，加载速度就比较慢。所以我们把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就比较高效，也就是按需使用才下载。

使用步骤：

1.<img src="D:\work\jianGuoYun\work\demo\vue\imgs\路由懒加载syntax-dynamic-import方法插件Snipaste_2021-04-12_23-13-10.jpg" style="zoom:50%;" />



第二步 复制插件名字

<img src="D:\work\jianGuoYun\work\demo\vue\imgs\第二步 复制插件名字Snipaste_2021-04-12_23-19-46.jpg" style="zoom:50%;" />

第三步，在vueui中，搜索依赖：

<img src="D:\work\jianGuoYun\work\demo\vue\imgs\第三步在vueui搜索插件Snipaste_2021-04-12_23-22-52.jpg" style="zoom:50%;" />





第四步，在babel.config.js文件中的plugins数组添加对应的插件，注意哦，有引号

<img src="D:\work\jianGuoYun\work\demo\vue\imgs\第四步，在babel.config.js文件中的plugins数组添加对应的插件，注意哦，有引号Snipaste_2021-04-12_23-27-09.jpg" style="zoom:50%;" />



第五步，对路由进行改造

<img src="D:\work\jianGuoYun\work\demo\vue\imgs\第五步，对路由进行改造Snipaste_2021-04-12_23-49-39.jpg" style="zoom:50%;" />

第六步，重新进行npm run build

















### tips:webpack报错bug解决方法

#### 1.Module not found: Error: Can't resolve './test.css' in 'D:\sync of jianGuo\npmModularity\src'

往往是该文件路径出现了错误，改成了../test.css解决BUG



webpack打包后的文件类似于一个加密文件，安全性高



#### 2.举例vue-elementUI-admin

### cnpm优化的下载方式

git clone之后不要cnpm i而是应该npm install --registry=https://registry.npm.taobao.org，这样可以规避一些Bug



#### 3.cnpm一直下nodeModules 一直下不好

重新装了node，卸载了cnpm,然后用npm install --registry=https://registry.npm.taobao.org的方法成功把所有的nodeModules下好了

#### 4.解决VSCODE"因为在此系统上禁止运行脚本"报错

找了下原因，是因为PowerShell执行策略的问题。

解决方法：

1. 以管理员身份运行vscode;
2. 执行：get-ExecutionPolicy，显示Restricted，表示状态是禁止的;
3. 执行：set-ExecutionPolicy RemoteSigned;
4. 这时再执行get-ExecutionPolicy，就显示RemoteSigned;
