---
title: ES6模块化
date: 2021-11-18 18:09:10
toc: true
top: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: 简述ES6模块化
tags:
- JavaScript
- Es6
---
# ES6模块化
ES6新增了模块化，包含两个部分，export与import，让JavaScript支持了module。

---

## 1. 默认暴露
 以暴露100为例，写法为
```
export defalut 100
```
 暴露的其实是一个**对象**，以default为属性，default后面的为值
 引入时的写法即为
```
// a = 100
import a form './xxx.js' 
```
完整的写法如下，其实是一个对象的解构，由于default是关键字不能直接解构，而且书写复杂，所以简化了写法。
```
import {default as a} from './xxx.js'
```
再比如如下写法
```
export default {
    a:100,
    b:10
}
```
暴露出去的其实是
```
{
    default:{
        a:100,
        b:10
    }
}
```
我们引入的时候如果写
```
import obj from './xxx.js'
```
那么`obj.a=100`,`obj.b=10`

>注意默认暴露只能写一次

---

## 2. 部分暴露
部分暴露出去的同样是对象，例如如下
```
export let a = 1;
export let obj = {
    a:10,
    b:100
}
```
那么暴露出去的对象为如下
```
{
    a,
    obj
}
```
所以引入的时候进行解构
```
import {a, obj} from './xxx.js'
// a = 1
// obj = {
    a:10,
    b:100
}
```

---

## 3. 整体暴露
整体暴露出去的同样是对象，如下例
```
let a = 1;
let obj = {
    a:10,
    b:100
}
export {a,obj}
```
export后面是什么，整体暴露出去的就是什么
引入方式和部分暴露一样

>其实整体暴露就是部分暴露的简化写法，不用再写那么多export罢了

---

## 4. 引入并暴露
我们可以通过例如`export { ... as ... } from "../xx/xx.js"`来进行引入并暴露。需要注意的是该模块相当于只转发了一下，它自身是不能直接使用引入的东西的。
如下例子，模块化写好API接口后需要整体挂载到VM的原型对象上
```
// 在index.js引入并暴露
export { default as trademark } from './product/trademark'
export { default as attr } from './product/attr'
export { default as category } from './product/category'
```

```
// 在main.js引入并挂载
import * as API from '@/api/index'
Vue.prototype.$API = API // 所有接口请求函数挂载到vue原型中
```

---

## 总结
1. 无论是什么方式暴露，暴露出去的都是对象，只不过对象的形成方式不同。默认暴露是以default为键，后面的值为值的对象。部分暴露是把所有暴露的变量封装到一个对象中，整体暴露是我们自己封装了对象暴露出去。
2. 无论是什么方式暴露，想要直接拿到暴露出去的对象（而不是解构的一部分）那么写法是
```
import * as obj from './xxx.js'
```
例如
```
export const a = ()=>{}
export const b = ()=>{}
import * as $API from './xxx.js'
// 使用函数
$API.a()
```