---
slug: vue-runtime-compiler
title: Vue的runtime与compiler
author: lightyisu
author_title: 
author_url: https://github.com/lightyisu
author_image_url: https://tvax4.sinaimg.cn/crop.0.0.1002.1002.1024/d1bdec9fly8gkzcigbeltj20ru0ruabm.jpg?KID=imgbed,tva&Expires=1606556341&ssig=Cu95rZ4khr
tags: [vue, runtime,compiler]
---
Vue的runtime与compiler
<img src='../static/img/vue_logo.png' height='30px'/>

<!--truncate-->
## vue的完全版=runtime(运行时)+compiler(编译器)

即

**完整版**：同时包含编译器和运行时的版本。

**编译器**：用来将模板字符串编译成为 JavaScript 渲染函数的代码。

**运行时**：用来创建 Vue 实例、渲染并处理虚拟 DOM 等的代码。基本上就是除去编译器的其它一切。


---


```js
// 需要编译器
new Vue({
  template: '<div>{{ hi }}</div>'
})
// 不需要编译器
new Vue({
  render (h) {
    return h('div', this.hi)
  }
})
```
编译器负责将template字符串模板转化为渲染函数后的vnode

**单文件:**

单vue文件则不需要在构建后引用完整版，因为打包后已经被编译成vnode

当使用 vue-loader 或 vueify 的时候，*.vue 文件内部的模板会在构建时预编译成 JavaScript。你在最终打好的包里实际上是不需要编译器的，所以只用运行时版本即可。


---


当使用`vue-loader`或`vueify`的时候，`*.vue`文件内部的模板会在构建时预编译成 JavaScript。你在最终打好的包里实际上是不需要编译器的，所以只用运行时版本即可。

因为运行时版本相比完整版体积要小大约 30%，所以应该尽可能使用这个版本。如果你仍然希望使用完整版，则需要在打包工具里配置一个别名

```js
module.exports = {
  // ...
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js' // 用 webpack 1 时需用 'vue/dist/vue.common.js'
    }
  }
}
```
**link⚡**
vue单文件中若使用template选项(option级)可由cli中的vue.config.js的runtimeCompiler选项开启，此时最终的构建文件引入的vue会加入编译器使得选项字符串模板可行(但需要解除单文件`<template>`)，若不开启编译器，则template选项级无效

