---
title: this的指向问题
date: 2021-12-01 16:55:24
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: 常见情况this的指向问题
tags:
  - JavaScript
---

# this 的指向问题

---

## 1. 直接调用函数

this 指向 window

```
function fn(){
    console.log(this)
}
fn();  // window
```

---

## 2. 构造函数中的 this

this 指向创建的实例对象 ff

```
function F1(){
    console.log(this)
}
const ff = new F1();
```

---

## 3. 通过对象调用

this 指向调用的人（谁调用指向谁）

```
const obj = {
    fn(){
        console.log(this)
    }
}
obj.fn() // obj
```

---

## 4. fn.call/apply(obj) 方法调用

this 指向传入的参数。这两个方法可以改变内部 this 的指向**并调用 fn 方法**

```
const obj1 = {};
const obj2 = {
    fn(){
        console.log(this)
    }
}
obj2.fn.call(obj1) // obj1
```

---

## 5. fn.bind(obj) 方法调用

this 指向传入的参数。这个方法可以改变内部 this 的指向**但是不调用 fn 方法**

```
const obj1 = {};
const obj2 = {
    fn(){
        console.log(this)
    }
}
obj2.ff = obj2.fn.bind(obj1) // 注意要进行接收
obj2.ff() // obj1
```

---

## 6. 箭头函数的 this

箭头函数没有自己的 this,它指向外部作用域的 this

---

## 7. 回调函数的 this

- 定时器/ajax/promise/数组遍历相关方法的回调，this 指向 window
- Vue 控制的回调函数，this 指向组件的实例

---

## 8. 如何控制函数的 this

- 利用函数的 bind()
- 利用箭头函数
- 用外部保存 this 如`const that = this`再去内部使用`that`
