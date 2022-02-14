### 过滤器filter

1. 过滤器可以用在双花括号插值和v-bind表达式
2. 过滤器默认参数为表达式的值，即之前的操作链的结果

```
{ message | filterA }
<!-- filterA过滤器第一参数为message -->

{ message | filterA('arg1', arg2) }
<!-- filterA过滤器第一参数为message,第二参数为'arg1',第三参数为'arg2' -->
```
3.过滤器可以串联

```
{{ message | filterA | filterB }}
<!-- filterA 被定义为接收单个参数的过滤器函数，表达式 message 的值将作为参数传入到函数中。
然后继续调用同样被定义为接收单个参数的过滤器函数 filterB，将 filterA 的结果传递到 filterB 中 -->
```

- 局部过滤器,组件的选项中定义本地的过滤器

```
filters: {
    capitalize: function (value) {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1)
    }
}
```

- 全局过滤器（当全局过滤器和局部过滤器重名时，会采用局部过滤器。）
  
```
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
```
