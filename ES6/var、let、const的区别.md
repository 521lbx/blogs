### var、let、const的区别

var定义的变量

1. 顶层变量，也是全局变量
2. 变量提升
3. 可以多次声明
4. 在函数中var声明变量是局部的，不使用var是全局的

let定义的变量

1. 只在let所在的代码块中有效
2. 不存在变量提升
3. 暂时性死区
4. 不能重复声明

cons定义的变量

1. 变量为常量，变量指向的内存地址保存的数据不能改变
2. 声明时就要赋值