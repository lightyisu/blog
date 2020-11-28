---
slug: vue-admin-template
title: Vue-admin-template学习
author: lightyisu
author_title: 
author_url: https://github.com/lightyisu
author_image_url: https://tvax4.sinaimg.cn/crop.0.0.1002.1002.1024/d1bdec9fly8gkzcigbeltj20ru0ruabm.jpg?KID=imgbed,tva&Expires=1606556341&ssig=Cu95rZ4khr
tags: [vue, vue-admin]
---
记录vue-admin-template学习
<img src='img/vue_logo.png' height='30px'/>

<!--truncate-->

## SVG-SPRITE

项目中的icon

iconfont中产生的iconfont.js是已经具有symbol标签的svg文件

只需要使用此js文件

在项目中使用`<use xlink:href='#icon-xxx'></use>`

引用即可

而真正需要单个svg只有路径的svg文件使用此use的话

需要将多个svg组合成一堆symbol标签

使用`<use>`引用这些symbol

而具有这些symbol的整体svg成为**svg sprite**

**可以通过**[svg-sprite-loader](https://github.com/kisenka/svg-sprite-loader)制作

