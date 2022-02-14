### vue模块包分析工具

#### 安装

```
npm install --save-dev webpack-bundle-analyzer
```

### cli3配置（vue.config.js）

```
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
module.exports = {
  configureWebpack: {
    plugins: [
      new BundleAnalyzerPlugin()
    ]
  },

};
```

### package.json配置（在scripts中增加如下命令）

```
"analyz": "NODE_ENV=production npm_config_report=true yarn build-changeOrder"
```


