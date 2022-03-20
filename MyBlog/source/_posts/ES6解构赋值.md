---
title: ES6解构赋值
date: 2021-11-19 22:24:26
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
toc: true
top: true
summary: ES6解构赋值的相关知识
tags:
- JavaScript
- Es6
---
# ES6解构赋值

---

## 1.数组解构
ES6中允许从数组中提取值，按照对应的位置对变量进行复制。
```
let [ a, b, c ] = [ 1, 2, 3 ]
// a = 1, b = 2, c = 3 代替了 let a = arr[0]
// 如果解构不成功，变量的值就是undefined
let [ a, b, c ]=[ 1, 2 ]
// c = undefined
``` 

> 如果要避免拿到undefined，可以先给一个默认值如`let [ a, b, c = 10] = [ 1, 2 ]`，这样c的值依然是10而不是undefined

---

## 2.对象解构
对象解构允许我们使用变量的名字去匹配对象的**属性**，匹配成功则讲对象属性的值赋值给该变量
```
let person = {
    uname: 'zs',
    age: 18
}
let { uname, age } = person;
// uname = 'zs', age = 18 变量名与属性名成功匹配
let { tname, tage } = person;
// tname与tage都是undefined 变量名与属性名未能成功匹配
```
* 但是变量名也不一定必须与属性名匹配，我们可以进行修改。依然是上面的例子

```
let { uname:myName, age:Myage } = person;
// myName = 'zs', Myage = 18 成功修改了变量名
```

---

## 3. 交换变量
在解构赋值中可以直接进行变量的交换，不用再找一个中间变量了
```
let a = 1;
let b = 3;
[ a, b] = [ b, a ]
// a = 3, b = 1
```



