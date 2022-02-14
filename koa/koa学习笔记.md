### koa学习笔记

1. 调用app.use的顺序决定了中间件的顺序
2. router是为了处理url
3. bodyparser解析元素的request对象的body，并绑定到ctx.request.body中
  bodyparser必须在router之前被注册到app对象上
4. 设置跨域
  ```
  //设置跨域访问中间件
  app.use(async (ctx, next)=> {
    ctx.set('Access-Control-Allow-Origin', '*');
    ctx.set('Access-Control-Allow-Headers', 'Content-Type, Content-Length, Authorization, Accept, X-Requested-With , yourHeaderFeild');
    ctx.set('Access-Control-Allow-Methods', 'PUT, POST, GET, DELETE, OPTIONS');
    if (ctx.method == 'OPTIONS') {
      // post请求的请求确认
      ctx.response.body = {
        subCode: 'SUCCESS',
        msg: '',
        data: ''
      }
    } else {
      await next();
    }
  });
  ```
