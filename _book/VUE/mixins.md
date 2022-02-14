### mixins
- 1.data选项内部会进行递归合并，并在发生冲突时以组件数据优先。即:合并、同名变量组件覆盖mixins值
- 2.值为对象的选项，例如 methods、components 和 directives，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。
- 3.生命周期函数，同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。
- 4.自定义选项
    1. 默认策略,简单地覆盖已有值
    2. 使用Vue.config.optionMergeStrategies添加合并函数
    ```
    Vue.config.optionMergeStrategies.myOption = function (toVal, fromVal) {
        // 返回合并后的值
    }
    ```
    3. 对于多数值为对象的选项，可以使用与 methods 相同的合并策略：
    ```
    var strategies = Vue.config.optionMergeStrategies
    strategies.myOption = strategies.methods
    ```
