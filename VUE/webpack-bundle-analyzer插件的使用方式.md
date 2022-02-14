### webpack-bundle-analyzer插件的使用方式

#### 这是一个webpack的插件，需要配合webpack和webpack-cli一起使用。这个插件的功能是生成代码分析报告，帮助提升代码质量和网站性能

1. npm install --save-dev webpack-bundle-analyzer //安装webpack-bundle-analyzer

2. npm install cross-env –save -dev //解决 'NODE_ENV' 不是内部或外部命令，也不是可运行的程序或批处理文件 的报错 

```
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
/* webpack.base.conf.js文件中 */
module.exports = vuxLoader.merge(webpackConfig, {
  plugins: [
    new BundleAnalyzerPlugin({
      analyzerMode: "server",
      analyzerHost: "127.0.0.1",
      analyzerPort: 8888, // 运行后的端口号
      reportFilename: "report.html",
      defaultSizes: "parsed",
      openAnalyzer: true,
      generateStatsFile: false,
      statsFilename: "stats.json",
      statsOptions: null,
      logLevel: "info"
    })
  ]
});

/* package.json文件中 */
"scripts": {
  "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js --open --hot",
  "start": "npm run dev",
  "unit": "jest --config test/unit/jest.conf.js --coverage",
  "e2e": "node test/e2e/runner.js",
  "test": "npm run unit && npm run e2e",
  "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
  "build": "node build/build.js",
  "analyz": "cross-env NODE_ENV=production npm_config_report=true npm run build"
}
```

#### 运行

```
npm run analyz
```


