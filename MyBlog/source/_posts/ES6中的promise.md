---
title: ES6中的promise
date: 2021-11-24 22:45:42
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: promise的介绍及运用
tags:
  - JavaScript
  - ES6
---

# ES6 中的 promise

## 1.什么是 promise

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了`Promise`对象。

所谓 Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。 ————《ECMAScript 入门》 by 阮一峰

## 2.为什么要使用 promise

简单的来说，解决了之前回调中嵌套回调代码层层推进嵌套的“回调地狱”。

## 3.promise 的写法

```
const p = new Promise((resolve, reject) => {
    // 一些代码
    if (/* 异步操作成功 */) {
        resolve(value) //成功
    } else {
        reject(value) //失败
    }
})
```

`promise`中有的参数`resolve`与`reject`，都是函数型参数。他们分别代表了异步操作成功与失败，并且可以将失败/成功的值传递出去。
以下用一个 ajax 的例子来进行对比

- 不用 promise 的情况，回调复杂的话就会造成多层嵌套

```
function logRes(res) {
    console.log(JSON.parse(res));
}
function sendAjax() {
    const xhr = new XMLHttpRequest()
    xhr.open("get", 'https://api.apiopen.top/getJoke')
    xhr.send()
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status >= 200 && xhr.status < 300) {
                logRes(xhr.responseText); // 这里是成功发送请求后的callback
            }
        }
    }
}
```

- 使用了 promise 后链式结构更加清晰易读

```
function sendAjax() {
    return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest()
        xhr.open("get", 'https://api.apiopen.top/getJoke')
        xhr.send()
        xhr.onreadystatechange = function () {
            if (xhr.readyState === 4) {
                if (xhr.status >= 200 && xhr.status < 300) {
                    resolve(xhr.responseText)
                } else {
                    reject(xhr.status)
                }
            }
        }
    })
}
sendAjax().then(
    value => {logRes(value)},
    reason => {console.log(reason)}
)
```

## 4. promise 的基本流程

{% asset_img 1.png %}

未完待续
