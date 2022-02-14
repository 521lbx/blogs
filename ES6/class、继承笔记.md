### class、继承笔记
- 类的所有方法都定义在类的prototype属性上面，类内部定义的方法都是不可枚举的

- new是从构造函数生成实例对象的命令

    new.target属性返回new命令作用于的那个构造函数,如果构造函数不是通过new命令调用，new.target会返回undefined

- Class 内部调用new.target，返回当前 Class。子类继承父类时，new.target会返回子类

- 子类必须在constructor方法中调用super方法，否则新建实例时会报错

- 判断一个类是否继承了另一个类： Object.getPrototypeOf(A) === B;
- constructor是默认方法，如未显式定义会默认添加空的constructor，new命令生成实例时自动调用constructor，constructor默认返回实例对象即this，
- 显式定义在this上的是实例的属性，未显式定义在this上的都定义在原型上即定义在class上
- 类的所有实例共享一个原型对象
- 通过Object.getPrototypeOf获取实例的原型并为原型添加属性和方法，将影响这个类所有的实例
- __proto__并不是语言的特性，是浏览器厂商提供的私有属性



