---
title: Vue路由的两种模式
date: 2021-11-22 21:41:25
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: Vue注册路由时的hash模式与history模式区别
tags:
- VUE
- JavaScript
---
# Vue路由的两种模式
---
## 1. hash模式
### 1.1. 什么是hash值
对于一个URL来说，`#`及其后面的值就是hash值
```
https://pan.baidu.com/disk/home#list/vmode=list
```
那么`#list/vmode=list`就是哈希值
### 1.2. hash值的特点
hash值**不会**包含在http**请求**中，即：hash值不会带给服务器，即便是刷新
### 1.3 hash模式的特点
1. 地址中一直带有#，不美观
2. 地址若通过第三方手机app分享，app校验严格的话地址会被标记为不合法
3. 兼容性较好

---

## 2. history模式
* 相较于hash模式只能改变#后的URL片段，history模式给了前端自由，整个URL都可以修改

### 2.1 history模式的特点
1. 地址干净美观
2. 兼容性相比hash模式较差
3. 应用部署上线需要后端支持以解决页面服务端404的问题。

### 2.2 解决history模式404问题
history模式害怕的就是给服务器发送请求，比如刷新的时候是实实在在的请求服务器，刷新的时候如果服务器中没有URL对应的资源则会报错404.
对于niginx来说可以用以下方式解决
```
location / {
  try_files $uri $uri/ /index.html;
}
```
对于 Node.js/Express，考虑使用 connect-history-api-fallback 中间件
(解决方式除了ngingx，其他暂不是特别熟悉如何使用，后面如果学到了会补充上来。)
