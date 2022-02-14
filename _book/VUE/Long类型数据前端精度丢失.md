### Long类型数据前端精度丢失

- 1.前端接收时，加请求拦截，在拦截中获取response未转json的初始数据，再做处理

```
instance.interceptors.response.use(response => {
    console.log(JSON.parse(response.request.response));
}, err => {
});
```

- 2.前端向后台发送时发送字符串，后台自动转long型

