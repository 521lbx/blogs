### directive自定义指令

注册全局的自定义指令
```
Vue.directive('focus', {
    // 当绑定的元素插入到DOM中时
    inserted: function (el) {
        // 聚焦元素
        el.focus();
    }
})
```

注册局部的自定义指令,<font color='red'>(组件中也接受一个 directives 的选项)</font>
```
directives: {
    focus: {
        // 指令的定义
        inserted: function (el) {
            el.focus();
        }
    }
}
```

在模板中任何元素上使用新的 v-focus 属性
```
<input v-focus>
```

自定义指令的钩子函数

- bind: 只调用一次，指令第一次被绑定到元素时调用（可以进行一次性的初始化设置）
- inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)
- update: 所在组件的 VNode 更新时调用(但是可能发生在其子 VNode 更新之前)
- componentUpdated: 指令所在组件的 VNode 及其子 VNode 全部更新后调用
- unbind: 只调用一次，指令与元素解绑时调用。

钩子函数的参数（除了 el 之外，其它参数都应该是只读的）

1. el: 指令所绑定的元素，可以用来直接操作DOM
2. binding: 一个对象，包含以下属性：
 - name: 指令名，不包括v-前缀
 - value： 指令绑定的值，例如：v-my-directive="1 + 1" 中，绑定值为 2
 - oldValue: 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。
 - expression： 字符串形式的指令表达式， 例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"
 - arg：传递给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
3. vnode: Vue 编译生成的虚拟节点
4. oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

动态指令参数

```
v-mydirective:[argument]="value"
<!-- argument 参数可以根据组件实例数据进行更新 -->

new Vue({
  el: '#dynamicexample',
  data: function () {
    return {
      argument: 'left'
    }
  }
})
```