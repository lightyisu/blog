---
slug: vue-router-l
title: Vue-router学习
author: lightyisu
author_title: 
author_url: https://github.com/lightyisu
author_image_url: https://tvax4.sinaimg.cn/crop.0.0.1002.1002.1024/d1bdec9fly8gkzcigbeltj20ru0ruabm.jpg?KID=imgbed,tva&Expires=1606556341&ssig=Cu95rZ4khr
tags: [vue, vue-router]
---
Vue的router
<img src='img/vue_logo.png' height='30px'/>

<!--truncate-->

# **多个视图出口的命名视图**

使用多个命名视图时
`
`<router-view name='xxx'></router-view>`

```
let routes=[
    {path:"/xxx",components:{
      xxx:xxx,
      default:xxxa
    }}
]
```
component此时add s
## redirect重定向

重定向指的是"/a"重定向到"/b"

则访问/a直接跳转到/b


---


# 全局前置守卫

```javascript
const router = new VueRouter({ ... })
router.beforeEach((to, from, next) => {
  // ...
})
```
**当一个导航触发时，全局前置守卫按照创建顺序调用。守卫是异步解析执行，此时导航在所有守卫 resolve 完之前一直处于 等待中。**
## router.beforeEach（(to,from,next)=>{}）

* `to: Route`: 即将要进入的目标[路由对象](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1)
* `from: Route`: 当前导航正要离开的路由
* `next: Function`: 一定要调用该方法来 resolve 这个钩子。执行效果依赖`next`方法的调用参数。
    * `next()`: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 confirmed (确认的)。
    * `next(false)`: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到`from`路由对应的地址。
    * `next('/')`或者`next({ path: '/' })`: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向`next`传递任意位置对象，且允许设置诸如`replace: true`、`name: 'home'`之类的选项以及任何用在`router-link`的`to`prop或`router.push`中的选项。
    * `next(error)`: (2.4.0+) 如果传入`next`的参数是一个`Error`实例，则导航会被终止且该错误会被传递给`router.onError()`注册过的回调。

**若不使用next()方法 则无法进行下一个导航**

**to ,from**-两个路由**对象**

**next**-resolve解析钩子

## 路由记录

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      children: [
        {
          path: 'bar',
          component: Bar,
          // a meta field
          meta: { requiresAuth: true }
        }
      ]
    }
  ]
})
```
`routes`配置中的每个路由对象为 路由记录。路由记录可以是嵌套的
**当嵌套路由时 路由记录是多条的**

/foo/bar 匹配的路由记录为Array(2)（数组成员为路由记录对象）即守卫中的to中的**to.matched**

'/foo'与'/foo/bar'两条路由记录


---
## 

# 守卫

## 全局前置守卫 router.beforeEach((to,from,next)=>{})

## 全局解析守卫  router.beforeResolve((to,from,next)=>{})

## 全局后置钩子 router.afterEach((to,from)=>{})

## 路由独享守卫 routes:[{path:'/',component:...,beforeEnter:(to,from,next)=>{}}]

## 组件守卫

1. beforeRouteEnter(...)
2. beforeRouteUpdate(...)
3. beforeRouteLeave(...)

**其中**

`beforeRouteEnter`**是支持给**`next`**传递回调的唯一守卫******

#### next回调

通过传一个回调给`next`来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。

```plain
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```

