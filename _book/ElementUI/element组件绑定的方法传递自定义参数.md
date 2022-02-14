### element组件绑定的方法传递自定义参数

#### select 远程搜索绑定方法传递自定义参数

```
<el-select filterable :filter-method="(val) => {filterBodyPart(val, bpCheckItem);}" v-model='bpCheckItem.bodyPartName'>
    <el-option v-for='item in bpCheckItem.bodyPartList' :key='item.name' :label="item.name" :value="item.name">
    <span>{{ item.name }}</span>
    </el-option>
    <!-- <el-option v-for='(item, index) in bordyPartComboList' :key='index' :label="item.inputName" :value="item.inputName">
    <span>{{ item.inputName }}</span>
    <span class="combo-tag">组套</span>
    </el-option> -->
</el-select>


filterBodyPart (inputval, bpCheckItem) { // 搜索检查部位 inputval: 搜索词，bpCheckItem：当前的检查部位检查方法信息
    // inputval默认会有的搜索词参数
    console.log(2222, inputval, bpCheckItem);
}
```

