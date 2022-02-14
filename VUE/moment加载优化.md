### moment加载优化

#### 安装

```
npm install --save-dev moment-locales-webpack-plugin
```

#### 使用(vue.config.js)

```
const MomentLocalesPlugin = require('moment-locales-webpack-plugin');

configureWebpack: {
    plugins: [
        new MomentLocalesPlugin(),
    ]
}

```

