### Module
#### tree-shaking依赖的就是es6的module实现

1. 编译时就能确定模块的依赖关系、输入及输出的变量，静态加载或编译时加载，CommonJS和AMD都只能在运行时确定,
CommonJS输出的是值的拷贝，ES6模块输出的是值的引用
2. export显示指定输出的代码，import指定输入
3. 自动采用严格模式
4. export 逐一导出、批量导出、导出时重命名

  ```
  // 逐一导出
  export var firstName = '汤';
  export var lastName = '小花';
  export var year = '18';
  ```

  ```
  // 批量导出
  var firstName = '汤';
  var lastName = '小花';
  var year = '18';
  export { firstName, lastName, year };
  ```

  ```
  // 重命名导出
  var firstName = '汤';
  var lastName = '小花';
  var year = '18';
  export { firstName as firstName1, lastName as lastName1, year as year1 };
  ```

5. export语句输出的接口，与其对应的值是动态绑定关系，通过接口可以获取到模块内部实时得值
6. export语句可以在模块的任何位置，只要处于模块顶层，不能在块级作用域中
7. import命令加载模块中变量，加载后变量只读，但可以改写变量的属性，其他模块也能读取到改写后的值
8. 加载时使用as为变量重命名

  ```
  import { lastName as surname } from './profile.js';
  ```

9. import命令具有提升效果，from后的路径可以是相对路径也可以是绝对路径，若只有文件名不带路径需有配置文件指定路径
10. import是静态执行，所以不能使用表达式或变量
11. import会执行加载的模块，singleten模式，多次加载只会执行一次

  ```
  // 仅执行但不输入任何变量
  import 'lodash';

  // 加载两次，但是只执行一次
  import { foo } from 'my_module';
  import { bar } from 'my_module';
  // 等同于
  import { foo, bar } from 'my_module';
  ```
12. 模块的整体加载
  ```
  // circle.js

  export function area(radius) {
    return Math.PI * radius * radius;
  }

  export function circumference(radius) {
    return 2 * Math.PI * radius;
  }
  ```

  加载circle.js

  ```
  import { area, circumference } from './circle';
  // 整体加载
  import * as circle from './circle';
  // circle应该是可以静态分析的，所以不允许运行时改变,circle的属性也不可以改
  ```
13. export default命令为模块指定默认输出，import加载时不使用大括号
  ```
  // export-default.js
  // 匿名函数前
  export default function () {
    console.log(123);
  }
  // 非匿名函数前（foo函数的函数名foo，在模块外部是无效的。加载的时候，视同匿名函数加载。）
  export default function foo () {
    console.log(123);
  }
  // import-default.js
  import customName from './export-default'
  ```
14. 一个模块只能有一个默认输入，因此export default命令只能使用一次
15. export default命令其实是输出一个叫default的变量，所有后面不能跟变量声明语句
16. 一条import语句同时输入默认方法和其他接口
  ```
  import defaultName, { a, b } from 'lodash'
  ```
17. export 和 import的复合写法
  ```
  export { foo, bar } from 'my_module';
  // 简单理解为以下代码，不同的是上面语句foo、bar并未实际导入当前模块，只是对外转发这俩接口，所以当前模块并不能使用foo和bar
  import { foo, bar } from 'my_module';
  export { foo, bar };

  // 接口改吗
  export {foo as muFoo} from 'my_module';
  // 整体输出
  export * from 'my_module';
  // 具名接口改为默认接口输出
  export {foo as default} from 'my_module';
  // 默认接口改为具名接口输出
  export {default as foo} from 'my_module';
  ```

18. 模块的继承
  ```
  // circleplus.js
  // 输出circle模块的所有属性和方法
  export * from 'circle';
  ```

19. 跨模块的常量
  将所有的常量文件合并在index.js文件中进行导出，使用时直接加载index.js文件

20. import()函数可以实现动态加载（es2020）
  ```
  import('./myModule.js')
  .then(({export1, export2}) => {
    // ...·
  });
  ```

#### Module的加载实现

1. 浏览器加载es6模块,异步加载，等整个页面渲染完再执行，相当于加了defer属性

  ```
    <script type='module'></script>
  ```
2. 使用async属性会异步加载，并且加载完立即执行

  ```
    <script type='module'  async></script>
  ```
3. 利用es6模块顶层this等于undefined特性，可以判断当前代码是否在es6模块之中
  ```
  const isNotModuleScript = this !== undefined;
  ```
4. node.js加载es6模块，从 Node.js v13.2 版本开始，Node.js 已经默认打开了 ES6 模块支持
  node.js要求es6模块采用.mjs后缀文件名，如果不希望将后缀名改成.mjs，可以在项目的package.json文件中，指定type字段为module。
  ```
  {
    "type": "module"
  }
  ```
  一旦设置了以后，该目录里面的 JS 脚本，就被解释用 ES6 模块。CommonJS 脚本的后缀名都改成.cjs。如果没有type字段，或者type字段为commonjs，则.js脚本会被解释成 CommonJS 模块；
  .mjs文件总是以 ES6 模块加载，.cjs文件总是以 CommonJS 模块加载，.js文件的加载取决于package.json里面type字段的设置。
  ```
  {
    "type": "module", // 知道js文件的默认模块类型
    "main": "./src/index.js", // 指定模块加载的入口文件
    "export": {
      "./submodule": "./src/submodule.js", // 指定脚本或子目录的别名,优先级高于main字段
    }
  }
  ```
5. main 的别名
  exports字段的别名如果是.,就代表模块的主入口，优先级高于main，并且可以直接简写成exports字段的值。
  ```
  {
    "exports": {
      ".": "./main.js"
    }
  }

  // 等同于
  {
    "exports": "./main.js"
  }
  ```

