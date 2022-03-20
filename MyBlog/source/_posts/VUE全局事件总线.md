---
title: VUE全局事件总线
date: 2021-11-20 21:56:37
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: VUE中全局事件总线的注册与使用
tags:
- VUE
- JavaScript
---
# VUE全局事件总线

---

## 1. 什么是全局事件总线
全局事件总线是一种**组件间通信**的方法。使用全局事件总线就可以不拘泥于父子组件或兄弟组件，任意的组件之间都可以进行通信。
那么如何达到在任意组件之间进行通信呢？我们就需要一个所有组件都能看得到的“人”，这个人当然就是VUE的原型对象。我们给它身上挂了东西，在我们创建了VC（VUE component）对象后，使用该东西的时候，组件顺着原型链查找，在这个组件中也可以用到这个东西。

---

## 2. 安装全局事件总线
由于是在VUE模型的原型对象上挂载，在`main.js`中就是如下写法
```
new Vue({
    .......
    beforeCreate(){
        Vue.prototype.$bus = this;
    },
    .......
})
```

---

## 3. 使用全局事件总线
1. 接收数据
A组件想要接收数据，那么就在A组件中给$bus绑定事件，**事件的回调留在A组件中**
```
methods: {
    ...
    callback(data){
        .....
    }
    ...
},
mounted(){
    this.$bus.$on('callback')
}
```
2. 传递数据
B组件需要传输数据给A组件，那么B组件中需要在合适的地方去触发这个事件
```
this.$bus.$emit('callback',data)
```
然后data就会被传递给A组件，同时A组间中的callback会被调用

---

## 3. 解绑事件
我们最好在`beforeDestroy`钩子中去解绑当前组件用到的事件。如下例
```
methods: {
    ...
    callback(data){
        .....
    }
    ...
},
mounted(){
    this.$bus.$on('callback')
},
beforeDestroy(){
    this.$bus.$off('callback')
    // 或者直接使用this.$bus.$off()不加任何参数来移除该组件的所有绑定事件
}
```