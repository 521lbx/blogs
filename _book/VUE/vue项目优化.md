### vue项目优化

- 1.组件使用懒加载

- 2.路由使用懒加载

- 3.vue打包开启gzip，nginx服务设置gzip
```
// vue.config.js中配置
const CompressionPlugin = require('compression-webpack-plugin');
configureWebpack: {
    plugins: [
      new CompressionPlugin({
        test: /\.js$|\.html$|.css/, // 匹配文件名
        threshold: 10240, // 对超过10k的数据进行压缩
        deleteOriginalAssets: false, // 是否删除源文件
      })]
},

// nginx配置

```

