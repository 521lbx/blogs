### slot
- 具名插槽

子组件base-layout内容：
```
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <!-- 未提供name,是默认插槽，默认name为default -->
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```
父组件使用：
```
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>
  <!-- 此内容将渲染至默认插槽里start -->
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>
  <!-- 此内容将渲染至默认插槽里end -->

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```
<font color='red'>注意 v-slot 只能添加在 template 上（除当被提供的内容只有默认插槽外）</font>
- 作用域插槽-->插槽 prop

   * 作用：让插槽内容能够访问子组件中才有的数据是

   * 语法：

 ```
 <!-- 子组件 -->
 <span>
  <slot v-bind:user="user">
    {user.lastName}
  </slot>
 </span>
 <!-- 父组件 -->
 <current-user>
  <template v-slot:default="slotProps">
    { slotProps.user.firstName }
  </template>
</current-user>
 ```
- 解构插槽 Prop（es6的解构赋值）

```
<current-user v-slot="{ user }">
  {{ user.firstName }}
</current-user>
<!-- 为插槽prop提供重命名 -->
<current-user v-slot="{ user: person }">
  {{ person.firstName }}
</current-user>
<!-- 为插槽 prop提供默认值，用于插槽 prop 是 undefined 的情形： -->
<current-user v-slot="{ user = { firstName: 'Guest' } }">
  {{ user.firstName }}
</current-user>
```

- v-slot的缩写：#
```
<base-layout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```
