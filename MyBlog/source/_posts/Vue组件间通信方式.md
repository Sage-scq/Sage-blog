---
title: Vue组件间通信方式
date: 2021-12-01 22:50:48
toc: true
categories: 前端知识 #文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
summary: Vue组件间通信方式的汇总
tags:
  - JavaScript
  - VUE
---

# Vue 组件间通信方式

---

## 1. 根据通信的组件间关系分类

- **父子组件**
  props
  vue 自定义事件
  v-model
  .sync
  $ref,$childre 与$parent
  插槽（作用域插槽）
- **祖孙组件**
  $attrs与$listeners
  provide 与 inject
- **任意组件间通信**
  全局事件总线
  Vuex

---

## 2.props

1. 实现父向子通信：属性值是非函数
2. 实现子向父通信：属性值是函数（不常用）

父组件中：

```
<blog-post :post="post"></blog-post>
```

子组件中：

```
props:['post']
```

或者对象写法：

```
props:{
    post:String
}
```

---

## 3. vue 自定义事件

用来实现子组件向父组件通信
父组件中绑定自定义事件监听:

```
<Child @eventName="callback">
```

子组件中分发事件

```
this.$emit('eventName', data)
```

---

## 4. 全局事件总线

实现任意组件间通信
将入口 js 中的 vm 作为全局事件总线对象:

```
beforeCreate() {
        Vue.prototype.$bus =this
    }
```

分发事件/传递数据的组件:

```
this.$bus.$emit('eventName', data)
```

处理事件/接收数据的组件:

```
this.$bus.$on('eventName', (data) => {})
```

---

## 5.v-model

1. 实现父子之间相互通信/同步
2. 组件标签上的 `v-model` 的本质: 动态 `value` 属性与自定义 `input` 监听来接收子组件分发的数据更新父组件数据

父组件:

```
<CustomInput v-model="name"/>
<!-- 等价于 -->
<CustomInput :value="name" @input="name=$event"/>
```

子组件：

```
<input type="text" :value="value" @input="$emit('input', $event.targetvalue)">
props: ['value']
```

---

## 6. .sync

1. 实现父子之间相互通信/同步(在原本父向子的基础上增加子向父)
2. 组件标签的属性上使用`.sync` 的本质: 通过事件监听来接收子组件分发过来的数据并更新父组件的数据

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

---

## 7. $attrs与$listeners

1. $attrs
    实现当前组件的父组件向当前组件的子组件通信
    它是包含所有父组件传入的标签属性(排除`props`声明, `class`与`style`的属性)的对象
    使用: 通过` v-bind="$attrs" `将父组件传入的 n 个属性数据传递给当前组件的子组件
2. $listeners
    实现当前组件的子组件向当前组件的父组件通信
    `$listeners `是包含所有父组件传入的自定义事件监听名与对应回调函数的对象 使用: 通过 `v-on="$listeners"` 将父组件绑定给当前组件的事件监听绑定给当前组件的子组件

---

## 8. $refs, $children, $parent

1. $refs
    实现父组件向指定子组件通信
    `$refs`是包含所有有`ref`属性的标签对象或组件对象的容器对象 使用: 通过`this.$refs.child` 得到子组件对象, 从而可以直接更新其数据或调用其方法更新数据
2. $children
    实现父组件向多个子组件通信
    `$children`是所有直接子组件对象的数组 使用: 通过`this.$children` 遍历子组件对象, 从而可以更新多个子组件的数据
3. $parent
    实现子组件向父组件通信
    `$parent`是当前组件的父组件对象 使用: 通过`this.$parent` 得到父组件对象, 从而可以更新父组件的数据

---

## 9. provide 与 inject

1. 实现祖孙组件间直接通信
2. 在祖组件中通过 `provide` 配置向后代组件提供数据
   在后代组件中通过 `inject` 配置来声明接收数据
3. 注意:
   不太建议在应用开发中使用, 一般用来封装 vue 插件
   provide 提供的数据本身不是响应式的 ==> 父组件更新了数据, 后代组件不会变化
   provide 提供的数据对象内部是响应式的 ==> 父组件更新了数据, 后代组件也会变化

---

## 10. Vuex

1. 实现任意组件间通信
2. Vuex 是一个专为 Vue 应用程序设计的管理多组件共享状态数据的 Vue 插件
   任意组件都可以读取到 Vuex 中 store 的 state 对象中的数据
   任意组件都可以通过 `dispatch()`或 `commit()`来触发 store 去更新 `state` 中的数据
   一旦 state 中的数据发生变化, 依赖于这些数据的组件就会自动更新

---

## 11. 插槽 ==> 作用域插槽 slot-scope

1. 实现父组件向子组件传递标签内容
2. 什么情况下使用作用域插槽?
   父组件需要向子组件传递标签结构内容
   但决定父组件传递怎样标签结构的数据在子组件中
3. 编码：

父组件:

```
 <template slot-scope="{row, $index}">
    <span>{{$index+1}}</span>nbsp;&nbsp;
    <span :style="{color$index%2===1 ? 'blue' 'green'}" >{{row.text}}</span>
</template>
```

子组件:

```
 <slot :row="item" :$index="index">  <!-- slot的属性会自动传递给父组件 --></slot>
```
