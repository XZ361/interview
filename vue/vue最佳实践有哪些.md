## 实际工作中，你总结的vue最佳实践有哪些？
---
1.编码风格方面：
- 命名组件时使用“多词”风格避免和HTML元素冲突
- 使用“细节化”方式定义属性而不是只有一个属性名
- 属性名声明时使用“驼峰命名”，模板或jsx中使用“肉串命名”
- 使用v-for时务必加上key，且不要跟v-if写在一起

2.性能方面：
- 路由懒加载减少应用尺寸
- 利用SSR减少首屏加载时间
- 利用v-once渲染那些不需要更新的内容
- 一些长列表可以利用虚拟滚动技术避免内存过度占用
- 对于深层嵌套对象的大数组可以使用shallowRef或shallowReactive降低开销
- 避免不必要的组件抽象

3.安全：
- 不使用不可信模板，例如使用用户输入拼接模板：template: `<div> + userProvidedString + </div>`
- 小心使用v-html，:url，:style等，避免html、url、样式等注入