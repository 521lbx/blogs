### $listeners、$attrs

#### $attrs--继承所有的父组件属性（除了prop传递的属性、class 和 style ）
#### inheritAttrs：默认值true,继承所有的父组件属性（除props的特定绑定）作为普通的HTML特性应用在子组件的根元素上，如果你不希望组件的根元素继承特性设置inheritAttrs: false,但是class属性会继承,注意 inheritAttrs: false 选项不会影响 style 和 class 的绑定。
#### $listeners--属性，它是一个对象，里面包含了作用在这个组件上的所有监听器，你就可以配合 v-on="$listeners" 将所有的事件监听器指向这个组件的某个特定的子元素。

