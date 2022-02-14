f### setTimeout第三参数

<font color='red'>此语法在ie9及以下不生效，需要polyfill</font>
```
// setTimeout、setInterval从第三位参数开始的参数，会在定时器到期时，作为第一位参数（函数）的参数传入
setTimeout((a, b) => {
    console.log(a); // 12
    console.log(b); // 15
}, 1000, 12, 15);
// 第三参数是setTimeout时会直接执行，5秒后doc变蓝，10秒后变红
setTimeout(function(){
    doc.style.color='red';
},10000,setTimeout(function(){
    doc.style.color='blue';
},5000));
```

