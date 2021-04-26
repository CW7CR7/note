# vue-router

先引入vue，在引入vue-router文件

<router-link to='/'>相当于

<a href='/'>

路由视图占位符：

<router-view>

创建路由实例对象

```js
const router=new VueRouter({
    //routes是一个对象数组，componet path redirect是比较常见的键名
    routes:[]
})
```

不要忘记把new出来的VueRouter对象挂载到Vue实例上面，否则就前功尽弃了