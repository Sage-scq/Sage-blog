---
title: 从0开始HTML5
date: 2021-11-19 21:21:00
toc: true
categories: 前端学习 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: 讲解HTML5新增的标签、特性等
tags:
- HTML5
- HTML
---

# 从0开始HTML5

---

## 1. HTML5新特性
HTML5的新特性主要是针对以前的不足，增加了一些新的标签、表单与属性。
这些特性都有兼容性问题，IE9以下需要慎重使用。

---

## 2.新增语义化标签
* `<header>`:头部标签
* `<nav>`:导航标签
* `<article>`:内容标签
* `<section>`:定义文档某个区域
* `<aside>`:侧边栏标签
* `<footer>`:尾部标签
{% asset_img 1.png %}
注意：
* 这种语义化标准主要是针对搜索引擎的
* 这些新标签可以在页面中多次使用
* 移动端没有兼容性问题，可以放心大胆的用

---

## 3. H5新增视频标签
* 语法
```
<video src="文件地址" controls="controls"></video>
```
* 可选属性
{% asset_img 2.png %}

---

## 4. H5新增音频标签
* 语法
```
<audio src="文件地址" controls="controls"></audio>
```
* 可选属性
{% asset_img 3.png %}

> 需要注意的是，Chrome浏览器是禁止音视频自动播放的

---

## 5. H5新增input
* 语法
```
<!-- 验证的时候必须添加form表单域 -->
<form action="">
    <ul>
        <li>邮箱：<input type="email"></input></li>
        <li>网址：<input type="url"></input></li>
        <li>日期：<input type="date"></input></li>
        <li>日期：<input type="time"></input></li>
        <li>数量：<input type="number"></input></li>
        <li>手机号码：<input type="tel"></input></li>
        <li>搜索：<input type="search"></input></li>
        <li>颜色：<input type="color"></input></li>
        <!--点击提交按钮就可以进行表单验证 -->
        <li><input type="submit"></input></li>
    </ul>
</form>
```
* 属性
{% asset_img 4.png %}

> 但是表单验证一般是自己写正则了，不一定用h5自带的这个

---

## 6. H5新增表单属性
* 语法
```
<input required="required"></input>
<input placeholder="请输入内容"></input>
<input autofocus="autofocus"></input>
<input autocomplete="off"></input>
<input type="file" multiple="multiple">
```
* 属性
{% asset_img 5.png %}

---

## 7. html常用实体符号
{% asset_img 6.png %}







