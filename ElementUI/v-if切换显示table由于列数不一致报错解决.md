### v-if切换显示table由于列数不一致报错解决
描述：页面多个el-table且table列数不一样时，切换table显示报错
_self.$scopedSlots.default is not a function
产生问题原因：
因为表格是element-ui通过循环产生的，而vue在dom重新渲染时有一个性能优化机制，就是相同dom会被复用，这就是问题所在，所以，通过key去标识一下当前行是唯一的，不许复用，就行了
解决1：
```
el-table上每个el-table-column加 :key="index + Math.random()"
```
解决2：
```
// 由于解决1会导致列表的排序状态无法正确切换，所以需要解决2。el-table上每个el-table-column无需改变

watch: {
    // 监听table传入的列的变化
    datacolumn () {
        // 先将列置空
      this.columns = [];
        // 延时赋上新的列数据，在触发表格重新布局
      setTimeout(() => {
        this.columns = this.datacolumn;
        this.$refs.tableList.doLayout();
      }, 10);
    }
  },
```

