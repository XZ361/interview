## 简述 Vue 的生命周期以及每个阶段做的事?
>每个Vue组件实例被创建后都会经过一系列初始化步骤，比如，它需要数据观测，模板编译，挂载实例到dom上，以及数据变化时更新dom。这个过程中会运行叫做生命周期钩子的函数，以便用户在特定阶段有机会添加他们自己的代码。
---
### What
1.Vue生命周期总共可以分为8个阶段：创建前后, 载入前后, 更新前后, 销毁前后，以及一些特殊场景的生命周期。**vue3中新增了三个用于调试和服务端渲染场景。**

| 生命周期v2    | 生命周期v3          | 描述                                     |
| ------------- | ------------------- | ---------------------------------------- |
| beforeCreate  | beforeCreate        | 组件实例被创建之初                       |
| created       | created             | 组件实例已经完全创建                     |
| beforeMount   | beforeMount         | 组件挂载之前                             |
| mounted       | mounted             | 组件挂载到实例上去之后                   |
| beforeUpdate  | beforeUpdate        | 组件数据发生变化，更新之前               |
| updated       | updated             | 数据数据更新之后                         |
| beforeDestroy | **beforeUnmounted** | 组件实例销毁之前                         |
| destroyed     | **unmounted**       | 组件实例销毁之后                         |
| activated     | activated           | keep-alive 缓存的组件激活时              |
| deactivated   | deactivated         | keep-alive 缓存的组件停用时调用          |
| errorCaptured | errorCaptured       | 捕获一个来自子孙组件的错误时被调用       |
| -             | **renderTracked**   | 调试钩子，响应式依赖被收集时调用         |
| -             | **renderTriggered** | 调试钩子，响应式依赖被触发时调用         |
| -             | **serverPrefetch**  | ssr only，组件实例在服务器上被渲染前调用 |

2.结合实践：

**beforeCreate**：通常用于插件开发中执行一些初始化任务

**created**：组件初始化完毕，可以访问各种数据，获取接口数据等

**mounted**：dom已创建，可用于获取访问数据和dom元素；访问子组件等。

**beforeUpdate**：此时`view`层还未更新，可用于获取更新前各种状态

**updated**：完成`view`层的更新，更新后，所有状态已是最新

**beforeunmounted**：实例被销毁前调用，可用于一些定时器或订阅的取消

**unmounted**：销毁一个实例。可清理它与其它实例的连接，解绑它的全部指令及事件监听器
3.`Vue`生命周期流程图：

![Component lifecycle diagram](https://gitee.com/57code/picgo/raw/master/lifecycle.cec11dcc.png)