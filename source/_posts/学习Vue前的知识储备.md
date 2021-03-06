---
title: 学习Vue前的知识储备
date: 2017-06-03 21:24:34
# description: 阶段
layout: post
tags: [Vue, 学习资料]
categories: 框架和库
---

## 架构知识储备
<!-- more -->
### 1. 模块化开发
推荐文章：
>* [前端模块化进程](https://www.zybuluo.com/wy/note/645263)
>* [浅谈前端模块化](http://imweb.io/topic/55994b358555272639cb031b)
>* js中的类和面向对象

### 2.webpack基础
推荐文章(了解即可)：
>* [webpack官方中文](https://doc.webpack-china.org/)
>* [webpack官方英文](https://webpack.github.io/docs/)
>* [Webpack中文指南](http://zhaoda.net/webpack-handbook/index.html)
>* [webpack简易入门](http://www.cnblogs.com/vajoy/p/4650467.html)
>* [入门 Webpack](https://segmentfault.com/a/1190000006178770)

### 3. ES6语法特性
推荐文章：
>* [EC6入门-阮一峰](http://es6.ruanyifeng.com/)
* [ES6十大新特性](http://www.alloyteam.com/2016/03/es6-front-end-developers-will-have-to-know-the-top-ten-properties/)

---
## vue知识储备
>目录中从**安装**到**组件**都需要了解，其中组件部分重点！！
[*Vue官方文档*](https://cn.vuejs.org/v2/guide/index.html)

最终需要搞明白
>包括但不仅限于
1. **了解** MVVM框架是什么？优势和解决的问题？
2. **了解** Vue实现数据双向绑定的原理？
3. **熟练** Vue实例所包含的属性和方法？
4. **熟练** Vue生命周期函数的运用？
5. **熟练** Vue中指令和运用？
6. **熟练** 表单控件的绑定？
7. **组件**中的data属性？
8. **组件**父子组件数据传递？
9. **组件**自定义事件作用？
10. **组件** slot内容分发？


### 1.vue实例
>* new Vue -- 实例化Vue，Vue是一个构造函数（面向对象）
* 选项对象 -- 包含数据、模板、挂载元素、方法、生命周期钩子等选项
* 属性和方法 -- 内置的一些方法（$）
* 钩子函数 -- 执行自定义逻辑

Vue实例中可能包含的属性和方法
```
var vm = new Vue({
  el: '#box',
    // 1.数据
  data: {
    a: 1
  },
    // 2.钩子函数
  created: function () {
    
  },
    // 3.计算属性
  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  },
    // 4.方法
  methods: {
  
  },
    // 5.观察
  watch: {
    question: function (newQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.getAnswer()
    }
  },
    // 6.模板
  template: 
    // 7.局部组件
  components:
  
  ...
})
```
生命周期
![](https://cn.vuejs.org/images/lifecycle.png)
### 2.模板语法
>* 虚拟DOM -- 在底层的实现上， Vue 将模板编译成虚拟 DOM 渲染函数
* 文本 -- {{ Mustache语法 }}
* 属性 -- v-bind 或者 v-model
* js单个表达式
* 指令 -- 表达式的值改变时相应地将某些行为应用到 DOM 上
* 修饰符
* 过滤器 -- 可以用在mustache插值和 v-bind 表达式，可串联

### 3.计算属性
>* 计算属性 -- 任何复杂逻辑，你都应当使用计算属性，对data进行逻辑处理
* 函数 -- return需要的东西
* computed vs methods -- 计算属性是基于它们的依赖进行缓存的
* computed vs Watched -- 更简便
* 计算属性可以分为get 和 set两个函数
* watch -- 数据变化响应时，执行异步操作或开销较大的操作

### 4.class和style绑定
>* 表达式的结果类型除了字符串之外，还可以是对象或数组
* :class=对象语法
* :class=数组语法
* :style=对象
* :style=数组 -- 可以将多个样式对象应用到一个元素
* CSS 属性名可以用驼峰式（camelCase）或短横分隔命名（kebab-case）
```
    // 对象语法
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
    // 数组语法
<div v-bind:class="[isActive ? activeClass : '', errorClass]">
    // :style=对象
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
    // :style=数组
<div v-bind:style="[baseStyles, overridingStyles]">
```
### 5.条件渲染
>* v-if && v-else && v-else-if
* 切换多个元素，可以把一个`<template>`元素当做包装元素
* v-show -- 切换display
* 当 v-if与v-for一起使用时，v-for 具有比 v-if 更高的优先级。

```
    // 高效复用，不会重新渲染相同元素，除非加不同的key属性
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>
```
### 6.列表渲染
>* v-for -- 指令根据一组**数组**的选项列表进行渲染
* v-for块中 -- 我们拥有对父作用域属性的完全访问权限
* v-for -- 支持一个可选的第二个参数为当前项的索引
* 数组 -- (item, index) in items
* 可以用of替代in作为分隔符，因为它是最接近 JavaScript 迭代器的语法 item of items
>* 也可以用 v-for 通过一个**对象**的属性来迭代
* 对象 -- 第二个的参数为键名，第三个参数为索引
* 整数 -- v-for="n in 10"
* v-for用在组件上，可以循环，但不能自动传递数据到组件里，防止耦合，因为组件有自己独立的作用域，为了传递迭代数据到组件里，我们要用 props
* v-for 的优先级比 v-if 更高
* v-for采用“就地复用” 策略，可以给元素添加唯一key值阻止
* 数组更新 -- 变异方法（能更改原始数组的方法）和非变异方法（不能改变原始数组的方法，重新赋值）


```
    // 向组件中传递数据
<my-component
  v-for="(item, index) in items"
  v-bind:item="item"
  v-bind:index="index">
</my-component>

    注意：由于 JavaScript 的限制， Vue 不能检测以下变动的数组
1. 当你利用索引直接设置一个项时，例如： vm.items[indexOfItem] = newValue
    解决：
        Vue.set(example1.items, indexOfItem, newValue)
    example1.items.splice(indexOfItem, 1, newValue)
2. 当你修改数组的长度时，例如： vm.items.length = newLength
    解决：
        example1.items.splice(newLength)
```


### 7.事件处理器
>* v-on -- （简写@）监听DOM事件
