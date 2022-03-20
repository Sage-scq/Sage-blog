---
title: css常用居中
date: 2021-11-19 01:44:59
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: 常用的css对齐方式
tags:
- css
---
# css常用居中
css中，对齐是经常要用到的，不论是水平还是垂直。

---

## 1.水平居中
### 1.1 元素水平居中
* 标准流块元素水平居中，一般使用`margin:auto;`。同时要设置元素的宽度，剩余的空间会在元素的两个外边距之间平均分配

>注意如果未设置宽度或宽度为100%，对齐会无效

```
.center {
  margin: auto;
  width: 50%;
  border: 3px solid green;
  padding: 20px;
}
```
* 非标准流需要使用position与transform配合进行居中

### 1.2 文字水平居中
* 文字水平居中的方式非常简单，即为`text-align:center;`
```
.center {
  text-align: center;
  border: 3px solid green;
}
```
{% asset_img 01.png %}

### 1.3 图像水平居中
* 图片要实现水平居中首先要将图片转换为**块元素**，再设置`margin:auto`即可
```
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 40%;
}
```

---

## 2. 垂直居中
### 2.1 元素垂直居中
* 可以给父元素使用`padding`进行居中（我很少用）
```
.center {
  padding: 70px 0;
  border: 3px solid green;
}
```
* 通常可以用`position`配合`transform`来进行垂直居中
```
.father { 
  height: 200px;
  position: relative;
  border: 3px solid green; 
}

.son  {
  margin: 0;
  position: absolute;
  left: 50%;
  transform: translateY(-50%);
}
```
* 使用flex布局实现垂直居中
```
center {
  display: flex;
  align-items: center;
  height: 200px;
  border: 3px solid green; 
}
```

### 2.2 文字垂直居中
* 一般文字垂直居中很简单，只需要让文字的行高等于盒子高度即可。
```
.box {
  height:200px;
  line-height:200px;
}
``` 

---

## 3. 图片和文字一行时垂直居中
* 可以给图片加上`vertical-align：middle`配合`line-height`一起使用
```
div {
  height: 200px;
  background-color: dodgerblue;
  line-height: 200px;
}
img {
  width: 600px;
  vertical-align: middle;
}
```
* 也可以给父元素`display:flex`两行代码解决问题
```
.father {
  display:flex;
  align-items:center;
}
```
