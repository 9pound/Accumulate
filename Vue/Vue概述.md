# Vue3.0 概述

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统



指令： 带有前缀 `v-`

`v-bind`

`v-on` 指令添加一个事件监听器

`v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定

v-if

v-for

## 组件化

是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用



components：组件注册





响应式模板和状态管理



`createApp` 函数创建一个新的应用实例、用来在应用中注册“全局”组件的

```js
const app = Vue.createApp({
  /* 选项 */
})

const app = Vue.createApp({})
app.component('SearchInput', SearchInputComponent)
app.directive('focus', FocusDirective)
app.use(LocalePlugin)
```

## 根组件

传递给 `createApp` 的选项用于配置**根组件**。当我们**挂载**应用时，该组件被用作渲染的起点。

根组件与其他组件没什么不同、配置选项是一样的，所对应的组件实例行为也是一样的。

```js
const RootComponent = { 
  /* 选项 */ 
}
const app = Vue.createApp(RootComponent)
const vm = app.mount('#app')
```

### 挂载

mount：把应用挂载到一个 DOM 元素中，返回的是根组件实例



## 组件实例 property

`data`

`methods`

`props`

`computed`

`inject`

`setup`

内置 property

$attrs

$emit



##  生命周期钩子

created



模板语法：允许开发者声明式地将 DOM 绑定至底层组件实例的数据、底层实现上、Vue 将模板编译成虚拟 DOM 渲染函数



### 模板语法

不用模板，也可以[直接写渲染 (render) 函数](https://v3.cn.vuejs.org/guide/render-function.html)，使用可选的 JSX 语法。



### 插值

文本插值

原始HTML插值

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

Mustache 语法不能在 HTML attribute 中使用，然而，使用 v-bind代替

如果绑定的值是 `null` 或 `undefined`，那么该 attribute 将不会被包含在渲染的元素上。

{{}} 中可以使用单个javaScript 表达式、HTML属性绑定中也可以使用

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```



## 指令：

指令 attribute 的值预期是**单个 JavaScript 表达式** (`v-for` 和 `v-on` 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

### 动态参数

```html
<a v-bind:[attributeName]="url"> ... </a>
```

### 修饰符

```html
<form v-on:submit.prevent="onSubmit">...</form>
```







## property

#### data 

组件的 `data` 选项是一个函数。Vue 会在创建新组件实例的过程中调用此函数。它应该返回一个对象，然后 Vue 会通过响应性系统将其包裹起来，并以 `$data` 的形式存储在组件实例中。

直接将不包含在 `data` 中的新 property 添加到组件实例是可行的。但由于该 property 不在背后的响应式 `$data` 对象内，所以 [Vue 的响应性系统](https://v3.cn.vuejs.org/guide/reactivity.html)不会自动跟踪它。

#### methods

Vue 自动为 `methods` 绑定 `this`，以便于它始终指向组件实例

在定义 `methods` 时应避免使用箭头函数，因为这会阻止 Vue 绑定恰当的 `this` 指向。



#### 计算属性：

对于任何包含响应式数据的复杂逻辑，你都应该使用**计算属性**。

计算属性只会在相关响应式依赖发生改变时重新求值。

每当触发重新渲染时，调用方法将**始终**会再次执行函数。

#### 侦听器：

`watch` 选项提供了一个更通用的方法来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

```html
 const watchExampleVM = Vue.createApp({
    data() {
      return {
        question: '',
        answer: 'Questions usually contain a question mark. ;-)'
      }
    },
    watch: {
      // 每当 question 发生变化时，该函数将会执行
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
      }
    },
```