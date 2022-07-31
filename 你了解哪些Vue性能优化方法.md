## 你了解哪些Vue性能优化方法？
---
- 1.最常见的路由懒加载：有效拆分App尺寸，访问时才异步加载
```
const router = createRouter({
  routes: [
    // 借助webpack的import()实现异步组件
    { path: '/foo', component: () => import('./Foo.vue') }
  ]
})
```
- 2.keep-alive缓存页面：避免重复创建组件实例，且能保留缓存组件状态
```
<router-view v-slot="{ Component }">
	<keep-alive>
  	<component :is="Component"></component>
  </keep-alive>
</router-view>
```

- 3.使用v-show复用DOM：避免重复创建组件
```
<template>
  <div class="cell">
    <!-- 这种情况用v-show复用DOM，比v-if效果好 -->
    <div v-show="value" class="on">
      <Heavy :n="10000"/>
    </div>
    <section v-show="!value" class="off">
      <Heavy :n="10000"/>
    </section>
  </div>
</template>
```
- 4.v-for 遍历避免同时使用 v-if：实际上在Vue3中已经是个错误写法
```
<template>
    <ul>
      <li
        v-for="user in activeUsers"
        <!-- 避免同时使用，vue3中会报错 -->
        <!-- v-if="user.isActive" -->
        :key="user.id">
        {{ user.name }}
      </li>
    </ul>
</template>
<script>
  export default {
    computed: {
      activeUsers: function () {
        return this.users.filter(user => user.isActive)
      }
    }
  }
</script>
```
- 5.v-once和v-memo：不再变化的数据使用v-once
```
<!-- single element -->
<span v-once>This will never change: {{msg}}</span>
```
   - 按条件跳过更新时使用v-momo：下面这个列表只会更新选中状态变化项
   ```
    <div v-for="item in list" :key="item.id" v-memo="[item.id === selected]">
    <p>ID: {{ item.id }} - selected: {{ item.id === selected }}</p>
    <p>...more child nodes</p>
    </div>
   ```

- 6.长列表性能优化：如果是大数据长列表，可采用虚拟滚动，只渲染少部分区域的内容
```
<recycle-scroller
  class="items"
  :items="items"
  :item-size="24"
>
  <template v-slot="{ item }">
    <FetchItemView
      :item="item"
      @vote="voteItem(item)"
    />
  </template>
</recycle-scroller>
```
- 7.事件的销毁：Vue 组件销毁时，会自动解绑它的全部指令及事件监听器，但是仅限于组件本身的事件。
```
export default {
  created() {
    this.timer = setInterval(this.refresh, 2000)
  },
  beforeUnmount() {
    clearInterval(this.timer)
  }
}
```
- 8.服务端渲染/静态网站生成：SSR/SSG
- 9.图片懒加载
>对于图片过多的页面，为了加速页面加载速度，所以很多时候我们需要将页面内未出现在可视区域内的图片先不做加载， 等到滚动到可视区域后再去加载。
`<img v-lazy="/static/img/1.png">`

- 10.第三方插件按需引入
>像element-plus这样的第三方组件库可以按需引入避免体积太大。
```
import { createApp } from 'vue';
import { Button, Select } from 'element-plus';

const app = createApp()
app.use(Button)
app.use(Select)
```

