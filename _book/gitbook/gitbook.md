### gitbook

#### 处理gitbook运行时报错
```
修改C:\Users\admin\.gitbook\versions\3.2.3\lib\output\website\copyPluginAssets.js文件，confirm: true改为confirm: false。
```

#### gitbook出现TypeError: cb.apply is not a function解决办法

打开polyfills.js文件（根据命令行报错路径找到此文件），在第62-64行调用了statFix这个函数,三行代码注释掉就解决报错了
```
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```

