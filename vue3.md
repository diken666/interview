# vue3

1. 如何理解vue3官网上说明的`渐进性`？
> 简单说，就是不做多余的操作，用你目前用得上的东西，需要哪些功能就引入哪些
2. vue3的生命周期函数对比 ![vue3与](./图片/vue3与vue2生命周期对比.png)
3. vue3生命周期图 及 父子组件挂载更新顺序
> ![vue3生命周期图](./图片/lifecycle-vue3.png)
> ```js
> // 组件挂载时
> // father setup
> // child setup
> // child mounted
> // father mounted
> // 子组件取消挂载后
> // father beforeUpdate
> // child beforeUnmount
> // child unmounted
> // father update
> ```
4. `props`和`data`哪个优先级高？
> 优先级 props -> methods -> data -> computed -> watch
>
5. 如何新建vue3项目并且支持tsx
> yarn create vite
> yarn add @vitejs/plugin-vue-jsx
> vite.config.ts 中引入 `@vitejs/plugin-vue-jsx` 并在`plugin`属性中使用
> tsconfig.json新增`"jsxImportSource": "vue"`
> `cmd + shift + p`选择`restart ts server`
6. vue的v-on如何绑定多事件
```vue
<div v-on="{click: func1, mousemove: func2}"></div>
<div @click="func1(),func2()}"></div>
```

