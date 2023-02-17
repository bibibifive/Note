# 前端框架(Vue & React)

### - [Vue](#Vue)
### - [React](#React)




# Vue

### 对 MVVM 模式的理解

MVVM 对应 3 个组成部分，`Model`（模型）、`View`（视图） 和 `ViewModel`（视图模型）。

- `View` 是用户在屏幕上看到的结构、布局和外观，也称 UI。
- `ViewModel` 是一个绑定器，能和 View 层和 Model 层进行通信。
- `Model` 是数据和逻辑。

### Vue 的[常用指令](https://cn.vuejs.org/api/built-in-directives.html)

| 指令             | 作用                                             |
| ---------------- | ------------------------------------------------ |
| v-text / `{{ }}` | 更新元素的文本内容。                             |
| v-html           | 类似 innerHTML                                   |
| v-show           | 比 v-if 开销小,不用直接删增 dom,用于频繁切换显隐 |
| v-if             | 是否渲染                                         |
| v-for            | 遍历渲染                                         |
| v-on / `@`       | 绑定事件监听                                     |
| v-bind / `:`     | 绑定属性                                         |
| v-model          | 用于表单绑定                                     |
| v-slot           | 具名插槽                                         |
| v-pre            | 跳过该元素及其所有子元素的编译。                 |
| v-once           | 只渲染一次                                       |
| v-memo           | 超级抠性能时用,用于跳过 diff                     |
| v-cloak          | 用于隐藏尚未完成编译的 DOM 模板。(一个占位内容)  |


### keep-alive

keep-alive 是 Vue 的内置组件，同时也是一个抽象组件，它主要用于`组件缓存`。当组件切换时会将组件的VNode缓存起来，等待下次重新激活时，再将缓存的组件VNode渲染出来，从而实现缓存。

常用的两个属性 include 和 exclude，支持字符串、正则和数组的形式，允许组件有条件的进行缓存。还有 max 属性，用于设置最大缓存数。

两个生命周期 activated 和 deactivated，在组件激活和失活时触发。

keep-alive 的缓存机制运用`LRU`(Least Recently Used)算法。


### Vue3 为什么使用 `Proxy` 代替 `Object.definedProperty`
Object.definedProperty 只能检测到属性的获取和设置，对于新增和删除是没办法检测的。在数据初始化时，由于不知道哪些数据会被用到，Vue 是直接递归观测全部数据，这会导致性能多余的消耗。

Proxy 劫持整个对象，对象属性的增加和删除都能检测到。Proxy 并不能监听到内部深层的对象变化，因此 Vue 3.0 的处理方式是在 getter 中去递归响应式，只有真正访问到的内部对象才会变成响应式，而不是无脑递归，在很大程度上提升了性能。


###　路由懒加载是如何实现的
动态加载
路由懒加载是性能优化的一种手段，在编写代码时可以使用 import() 引入路由组件，使用懒加载的路由会在打包时单独出来成一个 js 文件，可以使用 webpackChunkName 自定义包名。在项目上线后，懒加载的 js 文件不会在第一时间加载，而是`在访问到对应的路由时`，才会动态创建 script 标签去加载这个 js 文件。

```js
{
  path:'users',
  name:'users',
  component:()=> import(/*webpackChunkName: "users"*/ '@/views/users'),
}
```

### vue-router的原理
vue-router原理是更新视图而不重新请求页面。vue-router共有3种模式：`hash`模式、`history`模式、`abstract`模式。

- `hash`模式
hash模式使用 hashchange*监听地址栏的hash值*的变化，加载对应的页面。每次的hash值变化后依然会在浏览器留下历史记录，可以通过浏览器的前进后退按钮回到上一个页面。

- `history`模式
history模式*基于History Api实现*，使用 popstate 监听地址栏的变化。使用 pushState 和 replaceState 修改url，而无需加载页面。但是在刷新页面时还是会向后端发起请求，需要后端配合将资源定向回前端，交由前端路由处理。

- `abstract`
不涉及和浏览器地址的相关记录。通过数组维护*模拟浏览器的历史记录栈*。
























# React






## Hooks
`定义` 
系统运行到某一时期时，会调用被注册到该时机的回调函数。

`比较常见的钩子有：`
windows 系统的钩子能监听到系统的各种事件，
浏览器提供的 onload 或 addEventListener 能注册在浏览器各种时机被调用的方法。

`以 react 为例，hooks 是：`

一系列以 “`use`” 作为开头的方法，它们提供了让你可以完全避开 class式写法，在函数式组件中完成生命周期、状态管理、逻辑复用等几乎全部组件开发工作的能力。


`而在 vue 中， hooks 的定义可能更模糊：`
在 vue 组合式API里，以 “`use`” 作为开头的，一系列提供了组件复用、状态管理等开发能力的方法。

![React&Vue](./assets/前端框架/React&Vue.jpg#6)


### hooks命名规范

- 假设任何以 「`use`」 开头并紧跟着一个大写字母的函数就是一个 Hook。
- 只在 React 函数组件中调用 Hook，而不在普通函数中调用 Hook。（Eslint 通过判断一个方法是不是大坨峰命名来判断它是否是 React 函数）
- 只在最顶层使用 Hook，而不要在循环，条件或嵌套函数中调用 Hook。
- 因为是约定，因而 useXxx 的命名并非强制，你依然可以将你自定义的 hook 命名为 byXxx 或其他方式，但不推荐。

>因为约定的意义在于：我们不用细看实现，也能通过命名来了解一个它是什么。



