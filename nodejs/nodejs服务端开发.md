### nodejs服务端开发

1.编写服务文件server.js

```
'use strict'
var http = require('http');
var app = http.createServer(function(req,res) {
  res.writeHead(200, {'Content-Type':'text/platin'});
  res.end('Hello World');
}).listen('8080', '127.0.0.1');
// 使用netstat -ano查看端口监听状态
```

2.启动nodejs服务
  - 命令行执行node server.js
  - forever 启动

  ```
  // 安装forever
  npm install forever -g
  // forever启动服务
  forever start server.js
  // forever停止服务
  forever stop server.js
  ```
3. nodejs 热更新
  supervisor 可以帮助你实现这个功能，它会监视你对代码的改动，并自动重启 Node.js。
  安装
  ```
  npm install -g supervisor
  ``` 
  使用
  ```
  supervisor app.js
  ```
4. process全局变量，不需require可直接使用，提供当前Node.js进程的有关信息，并控制Node.js进程，process.argv 属性返回一个数组，这个数组包含了启动Node.js进程时的命令行参数