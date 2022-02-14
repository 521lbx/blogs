### 循环中使用computed属性提升性能

#### 向computed属性中传递参数以得到需要逻辑处理并可能会变化的循环绑定

```
<i :class='treeIcon({ node, data })'></i>
computed: {
  treeIcon () { // 处理模板树节点显示的图标
    return function ({ node, data }) {
      return `iconfont icon${
        data.category === 0
          ? (node.expanded ? 'fileclose_fill' : 'fileopen_fill')
          : 'doc_border'
      }`;
    };
  }
},
```

