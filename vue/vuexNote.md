## vuex的好处

1. 能够在vuex集中管理数据，易于开发和后期维护
2. 能高效实现组件之间的数据共享，提高开发效率
3. 存储在vuex中的数据都是响应式的。也就是说数据会自动的刷新，不需要程序员手动的同步



1. 需要组件之间传递的数据才需要放到vuex中，私有数据就放在data里面就行了。当然有时候所有数据全放在vuex中也是可以的，主要看具体的情况
2. vue ui进入识图化操作面板，然后找到项目管理器，新增项目
3. 包管理器选择npm

在安装项目过程中，vuex需要点击开启

vuex需要安装勾选的插件：

<img src="imgs\vuex需要安装勾选的插件Snipaste_2021-04-16_22-41-19.jpg" style="zoom:50%;" />

configuration :

<img src="imgs\configuration Snipaste_2021-04-16_22-42-50.jpg" style="zoom:50%;" />

下拉框选择：

ESLint+Standard config  也就是默认配置项



项目初始化之后呢，store.js就是vuex的导入文件



## state

比如state:{count:0}

#### 访问state数据第一种方法

全局访问：this.$store.state.count

视图层的话呢，当然可以这么写咯：{{$store.state.count}}。这是因为，在template标签里面，this是可以省略的



这个项目没有装vue-router

- cnpm install vue-router --save



记住咯，routes对象数组里面有path,component,redirect键名

完整项目的vue-router:

```js
// 路由
import Vue from "vue";
import VueRouter from "vue-router";
// import Login from "../components/Login.vue";
// import Home from "../components/Home.vue";
// import Welcome from '../components/Welcome.vue'
const Login = () => import(/* webpackChunkName: "login_home_welcome" */ '../components/Welcome.vue')
const Home = () => import(/* webpackChunkName: "login_home_welcome" */ '../components/Home.vue')
const  Welcome= () => import(/* webpackChunkName: "login_home_welcome" */ '../components/Welcome.vue')
// import Users from '../components/user/Users.vue'
// import Rights from '../components/power/Rights.vue'
// import Roles from '../components/power/Roles.vue'
const  Users= () => import(/* webpackChunkName: "users_rights_roles" */ '../components/Users.vue')
const  Rights= () => import(/* webpackChunkName: "users_rights_roles" */ '../components/Rights.vue')
const  Roles= () => import(/* webpackChunkName: "users_rights_roles" */ '../components/Roles.vue')
// import Category from '../components/goods/Category.vue'
// import Params from '../components/goods/Params.vue'
const  Category= () => import(/* webpackChunkName: "category_params" */ '../components/Category.vue')
const  Params= () => import(/* webpackChunkName: "category_params" */ '../components/Params.vue')
// import GoodsList from '../components/goods/List.vue'
// import GoodsAdd from '../components/goods/GoodsAdd.vue'
const  GoodsList= () => import(/* webpackChunkName: "goodsList_goodsAdd" */ '../components/GoodsList.vue')
const  GoodsAdd= () => import(/* webpackChunkName: "goodsList_goodsAdd" */ '../components/GoodsAdd.vue')
// import Order from '../components/order/Order.vue'
// import Report from '../components/report/Report.vue'
const  Order= () => import(/* webpackChunkName: "order_report" */ '../components/Order.vue')
const  Report= () => import(/* webpackChunkName: "order_report" */ '../components/Report.vue')

Vue.use(VueRouter);
const thisRouter = new VueRouter({
  routes: [
    { path: "/", redirect: "/login" },
    {
      path: "/login",
      component: Login
    },
    {
      path: "/home",
      component: Home,
      redirect: '/welcome',
      children: [{
        path: '/welcome',
        component: Welcome
      }, {
        path: '/users',
        component: Users
      }, {
        path: '/rights',
        component: Rights
      }, {
        path: '/roles',
        component: Roles
      }, {
        path: '/categories',
        component: Category
      }, {
        path: '/params',
        component: Params
      }, {
        path: '/goods',
        component: GoodsList
      }, {
        path: '/goods/add',
        component: GoodsAdd
      }, {
        path: '/orders',
        component: Order
      }, {
        path: '/reports',
        component: Report
      }]
    }
  ]
});
// 挂载路由守卫
// to,from,next是形参
thisRouter.beforeEach((to, from, next) => {
  if (to.path == "/login") {
    return next();
  }
  const tokenStr = window.sessionStorage.getItem("browserToken");
  if (!tokenStr) {
    next("/login");
  }
  next();
});
export default thisRouter;

```

#### 访问state第二种方法

要用state的组件首先

import {mapState} from 'vuex'

案例：

```js
比如state里面有个conut
要用他的组件：
逻辑层：
computed:{
    ...mapState(['count'])
}
视图层：
{{count}}
```

## mutation

用来变更store里面的数据

通过Mutation操作store里面的数据可能会有些繁琐，但是可以监控所有数据的变化。

举个栗子，比如有时候你想知道谁改变了state的数据，如果用state直接改变，就需要一个一个的翻组件找

基础用法

#### 第一种触发mutation的方式

```js
//有点像computed
mutations:{
    add(state){
        state.count++
    }
}
//需要用mutation的组件：
methods:{
    handle(){
        this.$store.commit('add')
    }
}
```

mutation里面的方法可以有第二个参数，这样可以更灵活

```js
const store=new Vuex.Store({
    state:{
        count:0
    },
    mutations:{
        //这里的n就是形参
        add2(state,n){
            state.count+=n
        }
    }
})
//需要用的组件：
methods:{
    handle2(){
        //4就是实参
        this.$store.commit('add2',4)
    }
}
```

#### 第二种触发mutations的方式

```js
import {mapState,mapMutations} from 'vuex'
如果要导入多个的话可以这么写：
import {mapMutations} from 'vuex'
```

通过刚才导入的mapMutations函数，将需要的mutations函数，映射为当前组件的methods方法

```js
methods:{
    ...mapMutations(['add','add2'])
}
```

mutations里面的函数有个问题，如果你写了异步的操作数据的方法，这个时候改变数据视图层变化但是控制台vue插件上显示没有变化

## action

这个是专门用来处理异步函数的。

但是action操作里，还是触发mutations里面的方法从而间接地改变数据

案例：

#### 第一种触发actions的方法

```js
const store=new Vuex.Store({
    mutations:{
        add(state){state.count++}
    },
    actions:{
        addAsync(con){
            setTimeout(()=>{
                con.commit('add')
            },1000)
        }
    }
})
组件：触发action 的第一种方法
methods:{
    handle(){
        this.$store.dispatch('addAsync')
    }
}
```

如果要携带参数

```js
定义action
const store=new Vuex.Store({
    mutations:{
        addN(state,n){
            state.count+=n
        }
    },
    actions:{
        addNAsync(con,n){
            setTimeout(()=>{
                con.commit('addN',n)
            },1000)
        }
    }
})
调用它的组件：
methods:{
    handle(){
        this.$store.dispatch('addNAsync',5)
    }
}
```

#### 第二种触发actions的方法：

```js
import {mapActions} from 'vuex'
#组件：也就是说把addASync从vuex里面映射到组件里的methods方法里面 思路和上面几个基本都一样。
methods:{
    ...mapActions(['addASync','addNASync'])
}
```

## getter

不修改源数据，会对store数据进行加工，类似vue里面的computed。

store里面的数据如果变化，那么getter里面的对应的数据也会跟着变化

#### 使用getters的第一种方法

```js
const store=new Vuex.Store({
    state:{
        count:0
    },
    getters:{
        showNum:state=>{
            return '当前的数量'+state.count
        }
    }
})
组件：
this.$store.getters.showNum
```

#### 使用getters的第二种方法

```js
import {mapGetters} from 'vuex'
computed:{
    ...mapGetters(['showNum'])
}
```

也就是说：

state,getter是映射到computed里面

mutation,action是映射到methods里面

安装ant-design

npm i vuex axios ant-design-vue -S