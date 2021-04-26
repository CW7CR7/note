schema://host:port/path?query#fragment

1. scheme:协议，比如http,https,ftp等
2. host:域名或者IP地址
3. port:端口,http默认80端口并且可以省略
4. path:路径，比如/index/title，可以是虚拟的路径，服务器可以并不存在这样的嵌套目录
5. query:查询参数，比如username=carlos&age=25
6. fragment:锚点（哈希HASH），用于定位页面的某个位置

前三个参数是必须要的



1. GET 查
2. POST 添加
3. PUT 修改
4. DELETE 删除

比如www.hello.com/books/123

就是PUT或者DELETE的形式的



### promise用法

```js
var p=new Promise((resolve,reject)=>{
        // 成功调用resolve 失败调用reject
    })
	//then里面可以放两个参数
    p.then(data=>{
        // 操作resolve的数据
    },error=>{
        // 操作reject得到的错误信息
    }).finally(data=>{
        // 操作不管成功或者失败得到的信息
    })
    // 第二种写法
    p.then(data=>{

    })
    .catch(err=>{})
    .finally(data=>{})
```

### then参数中的函数返回值

1. 返回promise实例对象
   - 返回的该实例对象会调用下一个then
2. 返回普通值
   - 返回的普通值会直接传给下一个then,通过then参数中的函数的参数接受该值

### promise实例方法

1. p.then()得到异步任务的正确处理结果
2. p.catch()获取异常信息
3. p.finally()成功与否都会执行

### promise对象方法

1. Promise.all()并发处理多个异步任务，所有任务都执行完成才能得到结果
2. Promise.race()并发处理多个异步任务，只要有一个任务完成就能得到结果



### fetch

#### get delete post put

相比于传统的AJAX更加的简单，基于promise的一个API，使用时候比较灵活，text()可以得到一个promise对象,当然也可以用json()来接受

```js
fetch(url).then(function(data){
        // text()方法属于fatchAPI的一部分，返回一个Promise实例对象，用于获取后台返回的数据
        return data.text();
    }).then(data=>{
        console.log(data);
    })
```

##### json()和text()方法之间的关系

```js
fetch(url).then(function(data){
        // text()方法属于fatchAPI的一部分，返回一个Promise实例对象，用于获取后台返回的数据
        return data.text();
    	//return data.json()
    }).then(data=>{
        console.log(data);
    	//这种写法就相当于上面的data.json(),如果写了上面这一步就可以省掉then后面的
    	var obj=JSON.parse(data);
    	console.log(obj)
    })
```



#### fetch的配置项：

1. method(String)：http请求方法：默认为GET(GET,POST,PUT,DELETE)
2. body(String):http的请求参数，如果是POST或者PUT，body必须要写配置的信息
3. headers(Object):http的请求头，默认为{}

#### get delete请求

后台接口：

```js
app.get('/books',(req,res)=>{
	//get请求使用query接受   前端路径： ?id=1
	res.send('接受的'+req.query.id)
})

app.get('/books/:id2',(req,res)=>{
	比如请求地址是    前端路径： /123
	//get请求使用params接受
	res.send('接受的'+req.params.id2)
})

app.delete('/books/:id2',(req,res)=>{
	比如请求地址是    前端路径： /123
	//del请求使用params接受
	res.send('接受的'+req.params.id2)
})
```

前端如果是get或者delete请求，只要通过fetch中的参数url来进行传递就可以了，例如：

?传参用query接受

/传参用params接受

```js
fetch('/books/123',{
    method:'delete'
}).then(data=>{
    return data.text()
}).then(data2=>{
	//这里才是最终的数据
    console.log(data2)
})
```



#### post请求

后台接口

```js
app.post('books',(req,res)=>{
    //body是中间件定义的
    res.send("接受的"+req.body.uname+'----'+req.body.pwd)
})
```

前端写法：

```js
fetch(url,{
        method:'post',
        body:'uname=carlos&pwd=123',
        headers:{
            'Content-Type':'application/x-www-form-urlencoded'
        }
    })
    .then(data=>data.text())
    .then(data=>console.log(data))
```

JSON形式传参POST

```js
fetch(url,{
        method:'post',
        body:JSON.stringify({
            uname:'carlos',pwd:'123'
        }),
        headers:{
            'Content-Type':'application/json'
        }
    })
    .then(data=>data.text())
    .then(data=>console.log(data))
```

#### put形式

和json传递类似 后面url路径需要这样写 比如 /123

后台接口 当然PUT传参也可以用'application/x-www-form-urlencoded' 和POST请求写法相当的类似

```js
app.put('books/:id',(req,res)=>{
    //body是中间件定义的
    res.send("接受的"+req.params.id+''+req.body.uname+'----'+req.body.pwd)
})
```



## axios

### 	概念：

axios是基于Promise用于浏览器和后端（node.js）的HTTP客户端

1. 支持浏览器和node.js
2. 支持promise语法
3. **能够拦截请求和响应**
4. **自动能转化JSON格式数据**（后台如果再传JSON格式数据，就可以免得转换了）

```js
<script src="./js/axios.js"></script>
<script>
    // url是后台接口地址
    // data是axios固定的写法,res可以随意命名
    axios.get(url).then(res=>console.log(res.data))
```

#### 三种请求携带数据的方法 GET

```js
// 第一种 后台通过query获取
    axios.get('/books?id=12')
    .then(res=>console.log(res.data))
    // 第二种 后台通过params获取
    axios.get('/books/12')
    .then(res=>console.log(res.data))
    // 第三种 用的最多的一种方法 后台通过query获取
    axios.get('/books',{
        params:{
            id:12
        }
    })
    .then(res=>console.log(res.data))
```

#### DELETE传参方法和上面的GET类似

三种方法对应的后台接口

```js
// 后台接口
    app.get('/data',(req,res)=>{
        res.send(req.query.id)
    })
    app.get('/data',(req,res)=>{
        res.send(req.params.id)
    })
    app.get('/data',(req,res)=>{
        res.send(req.query.id)
    })
```

#### POST请求方式

1.第一种：默认传递的格式是JSON格式的数据

```js
axios.post('/books',{
        params:{
            id:12,
            name:'carlos'
        }
    }).then(ret=>console.log(ret))
```

2.第二种：传递过来的是字符串形式的数据

```js
// 固定的API
    var params=new URLSearchParams()
    params.append('uname','carlos')
    params.append('pwd','123')
    axios.post(url,params).then(ret=>console.log(ret))
```

两种方式用哪种取决于后台，如果都可以用的话更加推荐第一种JSON形式的

#### PUT请求方式

和POST类似,后台接口路径需要加上/id(具体的值)

后台接口

```js
app.put('/data/:id',(req,res)=>{
        res.send(req.query.id)
    })
```

```js
axios.put('/books/123',{
        params:{
            id:12,
            name:'carlos'
        }
    }).then(ret=>console.log(ret))
```



### axios响应的结果

1. data:响应会来的数据
2. headers:响应头信息
3. status：响应状态码
4. statusText:响应状态信息

### axios的全局配置（常用）

1. axios.defaults.timeout=3000  //默认单位是毫秒

2. axios.defaults.baseURL='http://localhost:3000/'  //默认后台接口地址

   之后再发送请求的时候如果写'abc'就相当于http://localhost:3000/abc  (相当于在前面自动拼接了默认地址)

3. axios.defaults.headers['token']='djlksaljnm' //默认的请求头

后台接口需要配置一下请求头

```js
app.all('*',(req,res,next)=>{
        res.header('Access-Control-Allow-Origin','*')
        res.header('Access-Control-Allow-Methods','PUT,GET,POST,DELETE,OPTIONS')
        res.header('Access-Control-Allow-Headers','X-Requested-With')
        res.header('Access-Control-Allow-Headers','Content-Type')
        res.header('Access-Control-Allow-Headers','mytoken')
        next()
    })
```

# async await ES7带来的新特性

案例：

```js
async funciton queryData(id){
    //axios本质传递回来的是一个promise对象，promise对象本质就是一个异步的任务，所以可以在前面加上await。这样带来的好处就是不再需要then方法，或者是回调函数了，直接就拿到返回值
    const ret=await axios.get('/data')
    return ret;
}
	//如果上面写了返回
queryData().then(data=>{console.log(data)})
```

### 编辑 也就是增删改查中的改的时候，不能直接改

不能http://localhost:3000/books 通过表单信息改，因为有可能其他人也在进行修改，所以要用http://localhost:3000/books/:id来修改，确保改的时候就是最新的数据。也就是说页面上看到的数据有可能不是最新的



### vue router包含的路由功能

1. 支持html5历史模式或者hash模式
2. 支持嵌套路由
3. 支持路由参数
4. 支持编程式路由
5. 支持命名路由

注意vue-router是依赖于vue的，所以要先引入vue再引入vue-router

vue-router案例：默认的url地址是这样：file:///D:/sync%20of%20jianGuo/demo/vue/vueDemo/vueRouter.html#/user（hash地址）

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
    <div id="vueInside">
      <!-- 类似于a标签 -->
      <router-link to="/user">user</router-link>
      <router-link to="/register">register</router-link>
      <!-- router-view是占位符，router-link匹配到后，展示router-view里面的内容 -->
      <!--  -->
      <router-view></router-view>
    </div>
  </body>
  <script src="./js/vue.js"></script>
  <script src="./js/vue-router_3.0.2.js"></script>
  <script>
    const User = {
      template: `<div>
        <p>user</p>
        <button @click="goReg">跳转注册页面</button>
        <button @click="goBack">后退</button>
        <button @click="go1">测试</button>
        <button @click="go2">测试2</button>

        </div>`,
      methods: {
        goReg: function () {
          // this.$router.push('/register')
          this.$router.push("register");
        },
        goBack: function () {
          this.$router.go(-1);
        },
        go1: function () {
          this.$router.push({
            name: "nid",
            params: {
              nid: 55,
            },
          });
        },
        go2: function () {
          // url地址：/register?id=555
          this.$router.push({
            path: "/register",
            query: {
              id: 555,
            },
          });
        },
      },
    };
    const Kid1 = {
      template: `<p>kid1</p>`,
    };
    const Kid2 = {
      template: `<p>kid2</p>`,
    };
    const UserUid = {
      template: `<p>kidUID是{{$route.params.uid}}</p>`,
    };
    const UserPid = {
      props: ["pid", "name", "age"],
      template: `<div>
        <p>kidPID是{{pid}}</p>
        <p>名：{{name}}</p>
        <p>岁：{{age}}</p>
        </div>`,
    };
    const UserNid = {
      props: ["nid", "name", "age"],
      template: `<div>
        <p>kidnID是{{nid}}</p>
        <p>名：{{name}}</p>
        <p>岁：{{age}}</p>
        </div>`,
    };

    const Register = {
      template: `<div>
        <p>register</p>
        <!-- // 这种开头没有/就是相对路径，没有注释的就是绝对路径的url地址 -->
        <!-- <router-link to='register/kid1'>kid1</router-link> -->
        <!-- <router-link to='register/kid2'>kid2</router-link> -->
        <router-link to='/register/kid1'>kid1</router-link>
        <router-link to='/register/kid2'>kid2</router-link>
        <router-link to='/register/kid/1'>kidUID</router-link>
        <router-link to='/register/pid/1'>kidPID</router-link>
      <!-- 命名路由根据name直接找匹配的，必须加: -->
        <router-link :to="{name:'nid',params:{nid:88}}">nid</router-link>
      <router-view></router-view>
        </div>`,
    };

    // vuerouter实例
    var thisRouter = new VueRouter({
      routes: [
        {
          // 路由重定向 比如/访问 路径会自动变成/user 路径不区分大小写
          path: "/",
          redirect: "/User",
        },
        {
          // routes数组里path和component是必须参数
          path: "/user",
          component: User,
        },
        {
          path: "/register",
          component: Register,
          //路由数组 路由嵌套
          children: [
            {
              path: "/register/kid1",
              component: Kid1,
            },
            {
              path: "/register/kid2",
              component: Kid2,
            },
            {
              path: "/register/kid/:uid",
              component: UserUid,
            },
            {
              //   第一种props方式 开启路由传参
              //   props:true,
              //   箭头函数没有花括号就相当于return
              props: (route) => ({
                pid: route.params.pid,
                name: "carlos",
                age: 7,
              }),
              path: "/register/pid/:pid",
              component: UserPid,
            },
            {
              props: (route) => ({
                nid: route.params.nid,
                name: "carlos2",
                age: 8,
              }),
              path: "/register/nid/:nid",
              name: "nid",
              component: UserNid,
            },
          ],
        },
      ],
    });
    // vue实例对象
    var vueShili = new Vue({
      el: "#vueInside",
      // 路由必须要挂载到vue实例中才能使用
      router: thisRouter,
      methods: {},
    });
  </script>
</html>

```

