### js闭包

[菜鸟教程](https://www.runoob.com/js/js-function-closures.html)

#### 闭包是保护私有变量的一种机制，在函数执行时会形成私有作用域，保护私有变量不受外界干扰,直观的说就是形成一个不会销毁的栈环境

```
var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();
 
add();
add();
add();
 
// 计数器为 3

// 函数自我调用只会执行一次，设置计数器为0，并返回函数表达式。之后再执行就调用内层函数执行计数器加1，内层函数可以访问上层作用域的计数器。计算器匿名函数的保护，只能通过add函数修改
```

