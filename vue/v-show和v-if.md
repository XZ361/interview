# v-if/v-show


## v3/v2
- v-if按条件渲染，因为它确保了条件区块内的事件监听器和子组件都会在切换时被销毁与重建。
- v-if是懒加载的：如果在初次渲染时条件值为 false，则不会做任何事。条件区块会直到条件首次变为 true 时才渲染。
- v-show 简单许多，元素无论初始条件如何，始终会被渲染，仅作 CSS class 的切换。
- v-show 会在 DOM 渲染中保留该元素；v-show 仅切换了该元素上名为 display 的 CSS 属性

  (总的来说，v-if 在首次渲染时的切换成本比 v-show 更高。因此当你需要非常频繁切换时 v-show 会更好，而运行时不常改变的时候 v-if 会更合适。)