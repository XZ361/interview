## router-link和router-view是如何起作用的？
---
### What
- vue-router中两个重要组件router-link和router-view，分别起到路由导航作用和组件内容渲染作用

### How
- 使用router-link默认生成一个a标签，设置to属性定义跳转path。实际上也可以通过custom和插槽自定义最终的展现形式。
- router-view是要显示组件的占位组件，可以嵌套，对应路由配置的嵌套关系，配合name可以显示具名组件，起到更强的布局作用。

### Core
- router-link组件内部根据custom属性判断如何渲染最终生成节点，内部提供导航方法navigate，用户点击之后实际调用的是该方法，此方法最终会修改响应式的路由变量，然后重新去routes匹配出数组结果
- router-view则根据其所处深度deep在匹配数组结果中找到对应的路由并获取组件，最终将其渲染出来。