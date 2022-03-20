---
title: .sync运用————双向绑定多个属性
date: 2021-12-29 23:05:47
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: 常见情况this的指向问题
tags:
  - JavaScript
  - Vue
  - 前端知识
---

# .sync 运用————双向绑定多个属性

## 1. .sync 介绍

.sync 可以用于 vue 中子组件向父组件通信
通常用法如下
父组件:

```
<child :money.sync="total"/>
<!-- 等价于 -->
<Child :money="total @update:money="total=$event"/>

data () {
    return {
    total: 1000
    }
},
```

子组件：

```
<button @click="$emit('update:money', money-100)">花钱</button>
props: ['money']
```

## 2. .sync 如何进行多个属性的双向绑定

在公司写项目的时候遇到了这个问题，公用组件是别人封装好的，该组件有两个 input 框平行排列，双击左边的输入域会弹出一个 dialog，进行树形结构的选择。在选择一个节点后，该组件作者进行双向绑定的 @input 事件如下：

```
// 设置值并emit
selectCode(item, code, desc) {
    this.item = item
    this.codeVal = code
    this.descVal = desc
    // 双向绑定
    this.$emit('input', this.codeVal)
    // emit对象
    this.$emit('item', this.getItem())
},
```

可以看到，虽然`descVal`有值，但是输出的只有`codeVal`。
而我的需求是需要获取道`descVal`的值来发送请求，使用组件的代码如下

```
<template slot-scope="scope">
    <TreeCodeSelector v-model="scope.row.comCode" type="comCode" />
</template>
```

可以看到，v-model 只能获取到`codeVal`。
解决办法就是在公用组件中添加代码

```
// 设置值并emit
selectCode(item, code, desc) {
    this.item = item
    this.codeVal = code
    this.descVal = desc
    // 双向绑定
    this.$emit('input', this.codeVal)
    // .sync绑定comcName 新添加的语句
    this.$emit('update:comcname',this.descVal)
    // emit对象
    this.$emit('item', this.getItem())
},
```

那么在触发这个事件后，comcname 这个位于父组件的值就会更新，更新的值是我们传入的 descVal
父组件中的写法如下

```
<template slot-scope="scope">
    <TreeCodeSelector v-model="scope.row.comCode" type="comCode" :comcname.sync="scope.row.comcName" />
</template>
```

我们把`comcname`这个属性传给了`scope.row.comcName`，达到了目的。

> 这个方法会不会对没有写`:comcname.sync`的父组件产生影响报错还未实验。同时如果.sync 可以写多个的话，就达成了自定义组件的多个数据双向绑定，还是很有用的。
