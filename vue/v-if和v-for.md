# v-for / v-if一起使用

## 不推荐同时使用 v-if 和 v-for。
- v2:当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。
- v3:当 v-if 和 v-for 同时存在于一个元素上的时候，v-if 会首先被执行。

 在 Vue 2 中，v-for 优先于 v-if 被解析；但在 Vue 3 中，则完全相反，v-if 的优先级高于 v-for。
