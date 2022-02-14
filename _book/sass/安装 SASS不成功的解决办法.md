### 安装 SASS不成功的解决办法

```
npm install --save node-sass --registry=https://registry.npm.taobao.org --disturl=https://npm.taobao.org/dist --sass-binary-site=http://npm.taobao.org/mirrors/node-sass
npm rebuild node-sass --force
npm cache clean --force
```

